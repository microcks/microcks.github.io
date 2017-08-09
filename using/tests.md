---
layout: default
title: Executing tests
---

<div class="content">
	<div class="jumbotron clearfix">
		<div class="container">
       <h1 class="page-title arvo">Executing tests</h1>
    </div>
	</div>
  <div class="container">
    <section id="running-tests" class="article">
			<h2 class="arvo">Running tests</h2>
			<p>
				Microcks offers mocks but can also be used for <strong>Contract testing</strong> of API or services being under development. You spend a lot of time describing request/response pairs and matching rules: it would be a shame not to use this sample as test cases once the development is on its way!
			</p>
			<p>
				From the page displaying basic information on your <a href="../mocks/#mocks-info">microservice mocks</a>, you have the ability to launch new tests against different endpoints that may be representing different environment into your development process. Hitting the <b>NEW TEST...</b> button, leads you to the following form where you will be able to specify an target URL for test, as weel as a Runner - a testing strategy for your new launch :
			</p>
			<img src="../../assets/images/test-form.png" class="img-responsive"/>
			<p>
				<blockquote>
					While it is convenient to launch test 'on demand' manually, it may be interesting to consider launching new tests automatically when a new deployment of the application occurs for example... Microcks allows you such automation by offering API for ease of integration. See <a href="../../contributing/api/">here for more details</a>.
				</blockquote>
			</p>
		</section>

		<section id="test-runners" class="article">
			<h2 class="arvo">Different tests runners</h2>
			<p>
				As stated above, Microcks offers different strategies for runnning tests on endpoints where our microservice being developped should have been developped. Such strategies are implemented as <b>Test Runners</b>. Here are the default Test Runners available within Microcks:
			</p>
			<table class="table table-striped table-hover">
				<thead>
					<tr>
						<th>Test Runner</th>
						<th>API/Service Types</th>
						<th>Description</th>
					</tr>
				</thead>
				<tbody>
					<tr>
						<td><code>HTTP</code></td>
						<td>REST and SOAP</td>
						<td>Simplest test runner that only checks that valid target endpoints are deployed and available: returns a <code>20x</code> or <code>404</code> Http status code when appropriated. This can be called a simple "smock test".</td>
					</tr>
					<tr>
						<td><code>SOAP</code></td>
						<td>SOAP</td>
						<td>Extension of HTTP Runner that also checks that the response is syntaxically valid regarding SOAP WebService contract. It realizes a validation of the response payload using XSD schemas associated to service.</td>
					</tr>
					<tr>
						<td><code>SOAP_UI</code></td>
						<td>REST and SOAP</td>
						<td>When the microservice mock repository is defined using <a href="../soapui">SoapUI</a>: ensures that assertions put into Test cases are checked valid. Report failures.</td>
					</tr>
					<tr>
						<td><code>POSTMAN</code></td>
						<td>REST</td>
						<td>When the microservice mock repository is defined using <a href="../soapui">SoapUI</a>: executes test scripts as specified within Postman. Report failures.</td>
					</tr>
				</tbody>
			</table>
		</section>

		<section id="tests-history-details" class="article">
			<h2 class="arvo">Getting tests history and details</h2>

			<p>
				Tests history for an API/Service is easily accessible from the microservice <a href="../mocks/#mocks-info">summary page</a>. Microcks keep history of all the launched tests on an API/Service version. Success and failures are kept in database with unique identifier and test number to allow you to compare cases of success and failures.
			</p>
			<img src="../../assets/images/test-history.png" class="img-responsive"/>
			<p>
				Specific test details can be visualized : Microcks also records the request and response pairs exchanged with the tested endpoint so that you'll be able to access payload content as well as header. Failures are tracked and violated assertions messages displayed as shown in the screenshot below :
			</p>
			<img src="../../assets/images/test-details.png" class="img-responsive"/>
		</section>
  </div>
</div>
