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

<pre><code>{
  "service": {
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
        "dispatcherRules":"declare namespace ser='http://www.example.com/hello';\n//ser:sayHello/name",
        "defaultDelay":null,
        "resourcePaths":null
      }
    ]
  },
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
      {...}
    ]
  }
}
</code></pre>
	    </p>

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
		        <td><code>/services/{id}</code></td>
		        <td><code>id</code>: Unique identifier of this service</td>
		        <td>Get the details of the service: the full model shown above</td>
		      </tr>
				</tbody>
	    </table>
	  </section>

	  <section id="" class="article">
	    <h2 class="arvo">Tests API</h2>

			<h3 class="arvo">Model</h3>

			<p>
<pre><code>{
  "id":"5919d9014cedfd0001a5b61c",
  "testNumber":1,
  "testDate":1494866177868,
  "testedEndpoint":"http://10.130.6.226:8088/mockHelloService",
  "serviceId":"591463bed6018000012d1272",
  "elapsedTime":19,
  "success":true,
  "inProgress":false,
  "runnerType":"HTTP",
  "testCaseResults":[
    {
      "success":true,
      "elapsedTime":19,
      "operationName":"sayHello",
      "testStepResults":[
        {
          "success":true,
          "elapsedTime":16,
          "requestName":"Karla Request",
          "message":"200"
        },
        {
          "success":true,
          "elapsedTime":3,
          "requestName":"Andrew Request",
          "message":"200"
        }
      ]
    }
  ]
}
</code></pre>
			</p>

			<h3 class="arvo">Endpoint</h3>

	    Base : <code>http://host:port/api/tests</code>

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
						<td><code>POST</code></td>
						<td><code>/tests</code></td>
						<td><code>serviceId</code>: the unique id of Service to test, <code>testEndpoint</code>: the endpoint where Service to test has been deployed, <code>runnerType</code>: the type of test to run againts endpoint</td>
						<td>Create and launch a new test just with these 3 parameters. Uncomplete Test entity is returned with created <code>id</code>. Test is actually run asynchronously so you should call the <code>GET</code> method later to get test results</td>
					</tr>
		      <tr>
		        <td><code>GET</code></td>
		        <td><code>/tests/{id}</code></td>
		        <td><code>id</code>: Unique identifier of this test</td>
		        <td>Get the details of the test: the full model shown above</td>
		      </tr>
				</tbody>
	    </table>
	  </section>
  </div>
</div>
