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
			<img src="../../assets/images/postman-import.png" class="img-responsive, center-block" style="max-width: 60%"/>
			<p>
				After successful import and collection creation, you should get the following result into Postman: a valid Collection with a list of default requests created for your API paths and verbs. Elements of this list will be called <code>Operations</code> within Microcks. Here's the result for our <code>Test API</code>:
			</p>
			<img src="../../assets/images/postman-operations.png" class="img-responsive, center-block" style="max-width: 60%"/>
		</section>

		<section id="defining-examples" class="article">
			<h2 class="arvo">Defining Examples</h2>
			<p>
				As stated by Postman documentation :
			</p>
			<p>
				<quote><i>Developers can mock a request and response in Postman before sending the actual request or setting up a single endpoint to return the response. Establishing an example during the earliest phase of API development requires clear communication between team members, aligns their expectations, and means developers and testers can get started more quickly.</i></quote>
			</p>
			<p>
				The next step is now to create a bunch of examples for each of the requests/operations of your Collection as explained by the [Postman documentation](https://www.getpostman.com/docs/postman/collections/examples). You'll give each example a meaningful name regarding the use-case it supposed to represent. Do not forget to save your example!
			</p>
			<p>
				In contrary to [SoapUI usage](./soapui), you will not need defining mapping rules between sample requests and responses : example are perfectly suited for that.
			</p>
		</section>

		<section id="defining-tests" class="article">
			<h2 class="arvo">Defining Test Scripts</h2>
			<p>

			</p>
		</section>

		<section id="Save project" class="article">
			<h2 class="arvo">Export Postman collection</h2>
		</section>
	</div>
</div>
