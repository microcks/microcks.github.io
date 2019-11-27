---
layout: default
title: SoapUI usage for Microcks
---

<div class="content">
	<div class="jumbotron clearfix">
		<div class="container">
       <h1 class="page-title arvo">SoapUI usage for Microcks</h1>
    </div>
	</div>
  <div class="container">
    <section id="intro" class="article">
			<h2 class="arvo">Overview</h2>

			<h3 class="arvo">Pre-requisites</h3>
			<p>
				Microcks has been developped and tested with SoapUI version 5.x. It is recommend that you use a compatible version of this tool for editing your tests and mocks repository.
			</p>

			<h3 class="arvo">Steps for creating a repository</h3>
			<p>
				In order to create a tests and mocks repository using SoapUI, you'll need to follow the steps below:
				<ol>
					<li>Initialize a SoapUI project that will hold the repository,</li>
					<li>Create sample Tests Requests (and optionnally the associated tests assertions),</li>
					<li>Create sample Mocks Responses,</li>
					<li>Define dispatching rules that describe how requests and responses are associated together,</li>
					<li>Save the project into your SCM repository.</li>
				</ol>
			</p>

			<h3 class="arvo">Conventions</h3>
			<p>
				In order to be correctly imported and understood by Microcks, your SoapUI project should follow a little set of reasonable conventions and best practices.
				<ul>
					<li>Your SoapUI project may contain one or more Service definitions. However, because it's a best practice to consider each Service or API as an autonomous and isolated software asset, we'd recommend managing only one Service definition per SoapUI project,</li>
					<li>Your SoapUI Mock Service should define a custom property named <code>version</code> that allows tracking of Service(s) version. It is a good practice to change this version identifier for each Service or API interface versioned changes,</li>
					<li>The name of Tests Requests should be something like <code>"&lt;sample_id&gt; Request"</code>. For example: <code>"Karla Request"</code>,</li>
					<li>The name of Mock Responses should be something like <code>"&lt;sample_id&gt; Response"</code>. For example: <code>"Karla Response"</code>,</li>
					<li>The name of matching rules should be something like <code>"&lt;sample_id&gt;"</code>. For example: <code>"Karla"</code>,</li>
				</ul>
				We recommend having a look at our sample SoapUI projects for <a href="https://raw.githubusercontent.com/microcks/microcks/master/samples/HelloService-soapui-project.xml">SOAP WebServices</a> and for <a href="https://raw.githubusercontent.com/microcks/microcks/master/samples/HelloAPI-soapui-project.xml">REST APIs</a> to fully understand and see in action those conventions.
			</p>
		</section>

		<section id="project-intialisation" class="article">
			<h2 class="arvo">Project initialisation</h2>
			<p>
				Project initialization is as simple as creating a new <i>Empty Project</i> in SoapUI. The Tests Request you will need to define later will be defined through a <i>SoapUI TestSuite</i> ; the Mock Responses you will need to define later will be defined through a <i>SoapUI ServiceMock</i>. So when using a "contract first" approach for Services - approach that is required for SOAP WebServices in SoapUI - it is a better choice to directly create those items through the wizard when choosing the <i>Add WSDL</i> or <i>Add WADL</i> actions once project has been created.
			</p>
			<p>
				The screenshot below shows how to add a WSDL to an existing empty project :
			</p>
			<img src="../../assets/images/soapui-add-wsdl.png" class="img-responsive"/>

		</section>

		<section id="defining-tests" class="article">
			<h2 class="arvo">Defining Test Requests</h2>
			<p>
				The sample requests that are used by Microcks are indeed <i>SoapUI TestSuite</i> requests. So select the newly imported Service, right-click and choose <i>Generate TestSuite</i>. You should get this following screenshot where you select these options, validate and then give your TestSuite a name like <code>"&lt;Service&gt; TestSuite"</code> or something:
			</p>
			<img src="../../assets/images/soapui-create-testsuite.png" class="img-responsive"/>
			<p>
				You are now free to create as many <i>TestSteps</i> as you want within the <i>TestCases</i>. TestCases represents the <b>Operation</b> level and TestSteps represents the request sample level. The screenshot below shows how we have created 2 sample requests (<code>Andrew</code> and <code>Karla</code>) for the <code>sayHello</code> operation of our WebService:
			</p>
			<img src="../../assets/images/soapui-testrequest.png" class="img-responsive"/>
			<p>
				As shown above, you are also free to add some assertions within your TestStep requests. The SoapUI documentation introduces the assertion concept on <a href="https://www.soapui.org/functional-testing/assertion-teststep.html">this page.</a>. Assertions in TestSteps can be later reused when wanting to use Microcks for <a href="../tests/">Contract testing</a> of your Service.
			</p>
		</section>

		<section id="defining-mocks" class="article">
			<h2 class="arvo">Defining Mock Responses</h2>
			<p>
				Mock Responses you will need to define later will be defined through a <i>SoapUI ServiceMock</i>. You have to select the newly imported Service, right-click and choose <i>Generate MockService</i>. You can let the default options as shown below and give your MockService a name like <code>"&lt;Service&gt; Mock"</code>:
			</p>
			<img src="../../assets/images/soapui-create-servicemock.png" class="img-responsive"/>
			<p>
				You will now be able to create as many <i>Responses</i> attached to <i>Operation</i> as you've got samples requests defined in previously created <i>TestSteps</i>. As introduced into the naming conventions, your responses must have the same <code>"&lt;sample_id&gt;</code> radix that the associated requests so that Microcks will be later able to associate them.
			</p>
			<img src="../../assets/images/soapui-mockresponse.png" class="img-responsive"/>
			<p>
				The screenshot above shows a Mock response corresponding to the <code>Andrew Request</code>. It is simply code <code>Andrew Response</code>. Note that you are free to setup any HTTP Header you want for responses, Microcks will reuse them later to issue real headers in responses.
			</p>
		</section>

		<section id="defining-dispatch-rules" class="article">
			<h2 class="arvo">Defining dispatch rules</h2>
			<p>
				Latest step is now to define a technical mean for Microcks to analyse an incoming requests and find out the corresponding response to return. This is done in Microcks via the concept of <b>Dispatcher</b> that represent a dispatch strategy and <b>Dispatcher Rules</b> that represent the dispatching parameters. Microcks supports 2 strategies for dispatching SOAP requests:
				<ul>
					<li>Via the analysis of SOAP request payload through XPath,</li>
					<li>Via the evaluation of a Groovy script.</li>
				</ul>
				These two strategies have equivalent in SoapUI via Dispatch configuration on each Operation of your Mock Service.
			</p>

			<h3 class="arvo">Using XPath expression</h3>
			<p>
				After double-clicking on the operation node of your Mock Service, a window as shown in following screenshot should appear. If you want to use XPath for matching, select the <i>QUERY_MATCH</i> Dispatch and associate a <i>Mock Response</i> (upper section) with a new <i>Match Rule</i> (lower left) defining an XPath assertion (lower right). You can use the <i>Extract</i> helper in SoapUI if you're not familiar to XPath expression.
				<blockquote class="bg-warning">
					<small><b>Warning</b>: The XPath expression used by your different <i>Match Rule</i> must strictly be the same. You cannot used different expression for different rules.</small>
				</blockquote>
				Below the exemple of using the name find in incoming request to find a matching response.
			</p>
			<img src="../../assets/images/soapui-querymatch.png" class="img-responsive"/>

			<h3 class="arvo">Using a Groovy script</h3>
			<p>
				Another mean of defining matching rules is using a Groovy script. Such a script allows to define much more logic for finding a response for an incoming requests. With scripts you can use request payload but also have access to query string, http headers and so on... Groovy script are very powerful when dealing with REST services in SoapUI !
			</p>
			<img src="../../assets/images/soapui-script.png" class="img-responsive"/>
		</section>

		<section id="Save project" class="article">
			<h2 class="arvo">Save SoapUI project</h2>
			<p>
				Finally, you just have to save the whole project as a SoapUI XML project file. Just put the result JSON file into your favourite Source Configuration Management tool for an easy integration with Microcks.
				<blockquote class="bg-warning">
					<small>Do not forget to add the <code>version</code> custom property on your <i>MockService</i> object, otherwise Microcks will not be able to successfully import your SoapUI project.</small>
				</blockquote>
			</p>
		</section>
  </div>
</div>
