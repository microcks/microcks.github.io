---
layout: default
title: Postman usage for Microcks
---

<div class="content">
	<div class="jumbotron clearfix">
		<div class="container">
       <h1 class="page-title arvo">Postman usage for Microcks</h1>
    </div>
	</div>
	<div class="container">
    <section id="intro" class="article">
			<h2 class="arvo">Overview</h2>

			<h3 class="arvo">Pre-requisites</h3>
			<p>
				Microcks has been tested with latest version of Postman and uses the Collection  v2 format as input artifacts holding all your API mocks and tests definitions. Version 1 of the Collection format is actually not supported because it is not extensible and it is simply not where the community is heading.
			</p>

			<h3 class="arvo">Steps for creating a repository</h3>
			<p>
				In order to create a tests and mocks repository using Postman, you'll need to follow the steps below:
				<ol>
					<li>Initialize a Postman collection that will hold the repository,</li>
					<li>Create Examples and fill request parameters, headers and body,</li>
					<li>Describe associated response in terms of status, headers and body,</li>
					<li>Export the result as a JSON file using the Collection v2 format,</li>
					<li>Save the collection file into your SCM repository.</li>
				</ol>
			</p>

			<h3 class="arvo">Conventions</h3>
			<p>
			In order to be correctly imported and understood by Microcks, your Postman collection should follow a little set of reasonable conventions and best practices.
			<ul>
				<li>Your Postman collection may contain one or more API definitions. However, because it's a best practice to consider each API as an autonomous and isolated software asset, we'd recommend managing only one API definition per Postman collection and not mixing requests related to different APIs within the same Collection,</li>
				<li>Your Postman collection description should hold a custom property named <code>version</code> that allows tracking of API version. It is a good practice to change this version identifier for each API interface versionned changes. As of writing, Postman does not allow editing of such custom property although the Collection v2 format allow them. By convention, we allow setting it through the collection description using this syntax: <code>version=1.0 - Here is now the full description of my collection...</code>.</li>
			</ul>
			We recommend having a look at our sample Postman collection for <a href="https://raw.githubusercontent.com/microcks/microcks/master/samples/HelloService-soapui-project.xml">Test API</a> to fully understand and see in action those conventions.
			</p>
		</section>

		<section id="collection-intialisation" class="article">
			<h2 class="arvo">Collection initialisation</h2>
			<p>
				Collection initialization is done through <i>Import</i> of an existing resource into Postman. A best practice being using a "contract first" approach for API definition and management, you'll typically choose to <i>Import File</i> or <i>Import From Link</i> referencing a Swagger or OpenAPI contract definition.
			</p>
			<p>
				The screenshot below shows how to create a new collection from a Swagger file. We are using here the <a href="https://raw.githubusercontent.com/lbroudoux/apicurio-test/master/apis/test-api.json">Test API</a> Swagger file.
			</p>
			<img src="../../assets/images/postman-import.png" class="img-responsive, center-block" style="max-width: 50%"/>
			<p>
				After successful import and collection creation, you should get the following result into Postman: a valid Collection with a list of default requests created for your API paths and verbs. Elements of this list will be called <code>Operations</code> within Microcks. Here's the result for our <code>Test API</code>:
			</p>
			<img src="../../assets/images/postman-operations.png" class="img-responsive, center-block" style="max-width: 50%"/>
		</section>

		<section id="defining-examples" class="article">
			<h2 class="arvo">Defining Examples</h2>
			<p>
				As stated by Postman documentation :
			</p>
			<p>
				<blockquote><i>Developers can mock a request and response in Postman before sending the actual request or setting up a single endpoint to return the response. Establishing an example during the earliest phase of API development requires clear communication between team members, aligns their expectations, and means developers and testers can get started more quickly.</i></blockquote>
			</p>
			<p>
				The next step is now to create a bunch of examples for each of the requests/operations of your Collection as explained by the <a href="https://www.getpostman.com/docs/postman/collections/examples">Postman documentation</a>. You'll give each example a meaningful name regarding the use-case it supposed to represent. Do not forget to save your example!
			</p>
			<p>
				In contrary to <a href="./soapui#defining-dispatch-rules">SoapUI usage</a>, you will not need defining mapping rules between sample requests and responses : example are perfectly suited for that.
			</p>
		</section>

		<section id="defining-tests" class="article">
			<h2 class="arvo">Defining Test Scripts</h2>
			<p>
				[This is an optional step that is only required if you also want to use Microcks for testing your Service or API implement as the development process goes.]
			</p>
			<p>
			 	Postman allows to attach some test scripts defined in JavaScript to a request or <code>Operation</code>. Contrary to <a href="./soapui#defining-tests">SoapUI usage</a> where different tests assertions can be put on each test requests, Postman only allows you to attach script to the request level and not to examples. Such scripts should then be written so that they can be applied to the different examples but Microcks offers some way to ease that. For a global views of tests in Postman and their capabilities, we recommend reading the <a href="https://www.getpostman.com/docs/postman/scripts/intro_to_scripts">Introducting to Scripts</a>.
			</p>
			<p>
				As an illustration to how Microcks use Postman and offers, let's imagine we are still using the <a href="https://raw.githubusercontent.com/lbroudoux/apicurio-test/master/apis/test-api.json">Test API</a> we mentionned aboved. There's an <code>Operation</code> allowing to retrieve an order using its unique identifier. We have followed the previous section and have defined 2 examples for the corresponding request in Collection. Now we want to write a test that ensure that when API is invoked, the returned <code>order</code> has the <code>id</code> we specified into URI. We will write a test script that way:
			</p>
			<img src="../../assets/images/postman-script.png" class="img-responsive, center-block" style="max-width: 70%"/>
			<p>
				You will notice the usage of following JavaScript code: <code>var expectedId = globals["id"];</code>. What does that mean? Indeed, <code>globals</code> is an array of variables managed by Postman runtime. Usually, you have to pre-populate this array using <i>Pre-request script</i>. When running this tests in Microcks, such pre-request initialization are automatically performed for you! Every variable used within your request definition (URI parameters or query string parameters) are injected into the <code>globals</code> context so that you can directly used them within your script.
			</p>
			<p>
				The execution of Postman tests using Microcks follows this flow :
				<ul>
					<li>for each example defined for a request, collect URI and query string parameters as key/value pairs,</li>
					<li>inject each pair within <code>globals</code> JavaScript array,</li>
					<li>invoke request attached script with the <code>globals</code> injected into runtime context,</li>
					<li>collect the results within <code>tests</code> array to detect success or failure.</li>
				</ul>
				Here's below another example of such a generic script that validated the received JSON content:
			</p>
			<img src="../../assets/images/postman-script-validation.png" class="img-responsive, center-block" style="max-width: 70%"/>
			<p>
				This script validates that all the JSON <code>order</code> objects returned in response have all the <code>status</code> that is requested using the query parameter <code>status</code> value. Otherwise, a <code>Valid response</code> assertion failure is thrown and stored into the tests array.
			</p>
		</section>

		<section id="Save project" class="article">
			<h2 class="arvo">Export Postman collection</h2>
			<p>
				Finally, when you have defined all examples and optional test scripts on your requests, you should export your Collection as a JSON file using the Collection v2 format like shown below. Just put the result JSON file into your favourite Source Configuration Management tool for an easy integration with Microcks.
			</p>
			<img src="../../assets/images/postman-export.png" class="img-responsive, center-block" style="max-width: 50%"/>
		</section>
	</div>
</div>
