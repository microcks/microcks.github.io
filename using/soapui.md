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
					<li>Your SoapUI project may contain one or more Service definitions. However, because it's a best practive to consider each Service or API as an autonomous and isolated software asset, we'd recommend managing only one Service definition per SoapUI project,</li>
					<li>Your SoapUI project should define a custom property named <code>version</code> that allows tracking of Service(s) version. It is a good practice to change this version identifier for each Service or API interface versionned changes,</li>
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

			</p>
			<img src="../../assets/images/soapui-create-testsuite.png" class="img-responsive"/>
		</section>

		<section id="defining-mocks" class="article">
			<h2 class="arvo">Defining Mock Responses</h2>
			<p>

			</p>
			<img src="../../assets/images/soapui-create-servicemock.png" class="img-responsive"/>
		</section>

		<section id="defining-dispatch-rules" class="article">
			<h2 class="arvo">Defining dispatch rules</h2>

			<h3 class="arvo">Using XPath expression</h3>
			<p>
			</p>

			<h3 class="arvo">Using a Groovy script</h3>
			<p>
			</p>
		</section>

		<section id="Save project" class="article">
			<h2 class="arvo">Save SoapUI project</h2>
		</section>
  </div>
</div>
