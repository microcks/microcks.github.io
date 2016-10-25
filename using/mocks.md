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
    <section id="Infos on microservices" class="article">
			<h2 class="arvo">Getting infos on microservices mocks</h2>
		</section>

		<section id="" class="article">
			<h2 class="arvo">Invoking microservices mocks</h2>
		</section>

		<section id="" class="article">
			<h2 class="arvo">Common invocation params</h2>

			<table>
				<tr>
					<th>Param</th>
					<th>Type</th>
					<th>Description</th>
					<th>Default / Examples</th>
				</tr>
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
			</table>

			<p>
			This parameters may be used in addition of the Mock URL displayed on microservice informations page and should be append to the query URL. You may end up with URLs such as : `http://microcks.example.com/soap/HelloService/1.0/sayHello/?delay=250&validate=true`
			</p>
		</section>
	</div>
</div>
