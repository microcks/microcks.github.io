---
layout: default
title: Using exposed mocks
---

<div class="content">
	<div class="jumbotron clearfix">
		<div class="container">
       <h1 class="page-title arvo">Using exposed mocks</h1>
    </div>
	</div>
  <div class="container">
    <section id="mocks-info" class="article">
			<h2 class="arvo">Getting infos on microservices mocks</h2>
			<p>
				Well, now that you have <a href="./index.html">install</a> Microcks, created your own API/Service repository using <a href="../soapui/">SoapUI</a> or <a href="../postman/">Postman</a> and discover how to <a href="./index.html">import and browse content</a>, you are ready to learn more about how to use mocks managed by Microcks.
			</p>
			<p>
				First, let's have a look at the summary page presenting an API or Service managed by Microcks. This summary page contains three sections related to different part of the API/Service :
				<ul>
					<li><code>Properties</code> section show basic information on API/Service : its name, its version, its style (REST or SOAP) and you'll also got access to statistics regarding the utilization of the mocks of this API. SOAP style Service also contains extra information like the global <code>XML Namespace</code> used by the Service and the embedded <code>WSDL contract</code> if any was provided,</li>
					<li><code>Tests trend</code> section shows a little histogram representing the latest tests trend on this API/Service. It provides an access to test history and for launching a new test on an API/Service implementation. More on this topic in the <a href="./tests/">Tests documentation</a>,</li>
					<li><code>Operations</code> section concentrates informations on the different operations managed by this API or Service. More on that topic below.</li>
				</ul>
			</p>
			<img src="../../assets/images/mock-rest-summary.png" class="img-responsive"/>
			<p>
				Here's an example of summary page for a SOAP Service mock :
			</p>
			<img src="../../assets/images/mock-soap-summary.png" class="img-responsive"/>
			<p>
				Let's now focus on the <code>Operations</code> section of this page. A click on the operation name, unveil its details. Within an Operation panel, you will get generic information on this operation as well as visualization of typical request/response pairs examples (payload content and headers). 2 major informations should be isolated here are :
				<ul>
					<li>The <code>Mocks URL</code>: this is the URL fragment to which are exposed the mocks for this Operation of the API/Service. This fragment should be appended to your Microcks server URL to form a invokable URL. For example: <code>http://microcks-microcks.192.168.99.100.nip.io/rest/Test+API/0.0.1/order/:id</code>. When this URL contains variables part, this part is instanciated within each example panel,</li>
					<li>The <code>Dispatcher</code> and <code>Dispatching Rules</code> used by this operation. These elements are used by Microcks for finding an appropriate response to return receiving a mock request. It tells the user of the mocks what should be the immutable elements of his requests wether they may be located into the URL, the query string or the body payload. Microcks supports many dispatcher implementations whose names are rather self-explanatory. You may find: <code>URI_PARTS</code>, <code>URI_PARAMS</code>, <code>URI_ELEMENTS</code>, <code>QUERY_MATCH</code> or <code>SCRIPT</code></li>
				</ul>
			</p>
			<img src="../../assets/images/mock-details.png" class="img-responsive"/>
			<p>
				In the REST API mock example above, you can guess that the <code>:id</code> part of the Mock URL is used as the only criterion for finding accurate response when invoking mock. In the SOAP API mock example below, we use a much more elaborated dispatcher that is called <code>QUERY_MATCH</code> and uses the companion XPath expression provided as <code>Dispatching Rules</code> to extract from request payload the criterion for finding matching response.
			</p>
			<img src="../../assets/images/mock-soap-details.png" class="img-responsive"/>
		</section>

		<section id="mocks-invokation" class="article">
			<h2 class="arvo">Invoking microservices mocks</h2>
			<p>
				Invoking Mocks is now pretty easy if you have read the upper section! Just use Microcks for searching the API/Service you want to use and explore the operations of the API/Service. Find the Mock URL and the Http method of the corresponding operation, look at the instanciated URI fragement for different request/response pairs, append the fragment to the Microcks server url and that's it!
			</p>
			<p>
				As a rule of thumb, here is how the URL fragment for mocks are built and exposed within Microcks :
				<ul>
					<li>Mocks for REST API mocks are exposed on <code>/rest</code> sub-context. Mock for SOAP API mocks are exposed on <code>/soap</code> sub-context,</li>
					<li>Name of API/Service is then added as path element of URL. Special characters of name are encoded within URL part,</li>
					<li>Version of API/Service is then added as path element of URL,</li>
					<li>For REST API, name of resource managed by operation and URL parts may be added.</li>
				</ul>
			</p>
			<p>
				Some examples in the table below for a Microcks server reachable at <code>http://microcks.example.com</code> :
				<table class="table table-striped table-hover">
					<thead>
						<tr>
							<th>Type</th>
							<th>Name</th>
							<th>Version</th>
							<th>Operation / Parts / Params</th>
							<th>Full Mock URL</th>
						</tr>
					</thead>
					<tbody>
						<tr>
							<td>SOAP</td>
							<td>HelloService</td>
							<td>0.9</td>
							<td>"sayHello operation", NA</td>
							<td><code>http://microcks.example.com/soap/HelloService/0.9/</code></td>
						</tr>
						<tr>
							<td>REST</td>
							<td>Test API</td>
							<td>0.0.1</td>
							<td>"Find by id" operation, order resource, example with id=123456</td>
							<td><code>http://microcks.example.com/rest/Test+API/0.0.1/order/123456</code></td>
						</tr>
						<tr>
							<td>REST</td>
							<td>Test API</td>
							<td>0.0.1</td>
							<td>"List by status" operation, order resource, example with status=approved</td>
							<td><code>http://microcks.example.com/rest/Test+API/0.0.1/order?status=approved</code></td>
						</tr>
					</tbody>
				</table>
				Easy !?
			</p>
		</section>

		<section id="mocks-common-params" class="article">
			<h2 class="arvo">Common invocation params</h2>

			<table class="table table-striped table-hover">
				<thead>
					<tr>
						<th>Param</th>
						<th>Type</th>
						<th>Description</th>
						<th>Default / Examples</th>
					</tr>
				</thead>
				<tbody>
					<tr>
						<td><b>validate</b></td>
						<td>boolean</td>
						<td>In case of a SOAP microservice with defined WSDL/XSD contract, the mock may realize a validation of XML payload send by consumer if this parameter is set to true.</td>
						<td>Default is <b>false</b></td>
					</tr>
					<tr>
						<td><b>delay</b></td>
						<td>positive integer</td>
						<td>Set a response delay to simulate slow responding systems and check behavior of the service consumer being under tests. Note: this is an execution simulation response time: validation time and network latency are not taken into account</td>
						<td>Default is <b>0</b>. Use for example 1000, to have a 1 second delay on mock invocation</td>
					</tr>
				</tbody>
			</table>
			<p>
			This parameters may be used in addition of the Mock URL displayed on microservice informations page and should be append to the query URL. You may end up with URLs such as : <code>http://microcks.example.com/soap/HelloService/1.0/sayHello/?delay=250&validate=true</code>
			</p>
		</section>
	</div>
</div>
