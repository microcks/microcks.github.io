---
layout: default
title: Integrating Microcks using API
---

<div class="content">
	<div class="jumbotron clearfix">
		<div class="container">
       <h1 class="page-title arvo">Integrating Microcks using API</h1>
    </div>
	</div>
  <div class="container">
  <section id="" class="article">
    <h2 class="arvo">Services API</h2>

    <p>
    <h3 class="arvo">Model</h3>

    <pre><code>
{
	"id":"591463bed6018000012d1272",
	"name":"HelloService Mock",
	"version":"0.9",
	"xmlNS":"http://www.example.com/hello",
	"type":"SOAP_HTTP",
	"operations":[
		{
			"name":"sayHello",
			"method":null,
			"inputName":"sayHello",
			"outputName":"sayHelloResponse",
			"dispatcher":"QUERY_MATCH",
			"dispatcherRules":"declare namespace ser='http://www.example.com/hello';\n//ser:sayHello/name","defaultDelay":null,"resourcePaths":null}]},
			"messagesMap":{
				"sayHello":[
					{
						"request":{
							"name":"Karla Request",
							"content":"<soapenv:Envelope ...</soapenv:Envelope>",
							"operationId":"591463bed6018000012d1272-sayHello",
							"headers":null,
							"id":"5915bff04cedfd0001a5b60f",
							"responseId":"5915bff04cedfd0001a5b60d",
							"queryParameters":null
						},
						"response":{
							"name":"Karla Response",
							"content":"<soapenv:Envelope ...</soapenv:Envelope>",
							"operationId":"591463bed6018000012d1272-sayHello",
							"headers":null,
							"id":"5915bff04cedfd0001a5b60d",
							"status":null,
							"mediaType":null,
							"dispatchCriteria":"Karla",
							"fault":false
						}
					},
					{
						"request":{
							"name":"Andrew Request",
							"content":"<soapenv:Envelope ...</soapenv:Envelope>",
							"operationId":"591463bed6018000012d1272-sayHello",
							"headers":null,
							"id":"5915bff04cedfd0001a5b610",
							"responseId":"5915bff04cedfd0001a5b60e",
							"queryParameters":null
						},
						"response":{
							"name":"Andrew Response",
							"content":"<soapenv:Envelope ...</soapenv:Envelope>",
							"operationId":"591463bed6018000012d1272-sayHello",
							"headers":null,
							"id":"5915bff04cedfd0001a5b60e",
							"status":null,
							"mediaType":null,
							"dispatchCriteria":"Andrew",
							"fault":false
						}
					}
				]
			}
		}
	]
}
    </code></pre>
    </p>

    <p>
    <h3 class="arvo">Endpoint</h3>

    Base : <code>http://host:port/api/services</code>

    <table class="table table-striped table-hover">
      <thead>
				<tr>
	        <th>Verb</th>
	        <th>URL</th>
	        <th>Params</th>
	        <th>Description</th>
	      </tr>
			</thead>
			<tbody>
	      <tr>
	        <td><code>GET</code></td>
	        <td><code>/services/{id}</td>
	        <td><code>id</code>: Unique identifier of this service</td>
	        <td>Get the details of the service: the full model shown above</td>
	      </tr>
			</tbody>
    </table>
    </p>
  </section>

    <section id="" class="article">
      <h2 class="arvo">Tests API</h2>
    </section>
  </div>
</div>
