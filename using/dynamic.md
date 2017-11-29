---
layout: default
title: Getting dynamic mocks
---

<div class="content">
	<div class="jumbotron clearfix">
		<div class="container">
       <h1 class="page-title arvo">Getting dynamic mocks</h1>
    </div>
	</div>
  <div class="container">
    <section id="dynamic-mocks" class="article">
      <h2 class="arvo">Creating dynamic mocks</h2>
      <p>
        Eventhough Microcks promotes a contract first approach for defining mocks, we are well aware that in real-life it may be difficult starting that way without a great maturity on API and Service contracts. We often meet situations when design and development teams need to play a bit with a fake API to really figure out their needs and how they should then design API contract. In order to help with those situation, Microcks offers the ability to dynamically generate a generic API that you may use as a sandbox.
      </p>
      <p>
        In a few clicks, Microcks will easily generate for you a basic API with CRUD operations (CRUD for <i>Create-Retrieve-Update-Delete</i>) and associated mocks that you'll be able to use for recording, retrieving and deleting any type of JSON document. In order to use this "Backend As A Service" like feature, just go to the <b>Services</b> repository and hit the <code>Add Dynamic Service...</code> button:
      </p>
      <img src="../../assets/images/dynamic-link.png" class="img-responsive"/>
      <p>
        A simple form is now display, asking you to give the following Service Properties:<ul>
          <li><code>Service Name and Version</code></li> will be the unique identifiers of the new dynamic service you want to create,
          <li><code>Resource</code></li> will the kind of resource (as REST protocol understands <i>resource</i>) that will be manage by dynamic service.
        </ul>
      </p>
      <img src="../../assets/images/dynamic-form.png"/>
      <p>
        Just hit the <code>Add</code> button and you are few seconds away of having a ready-to-use REST Service/API that proposes different operations as shown in capture below. This Service/API is immediately exposing mocks endpoints for the different operations. It Swagger contract is also directly available for download.
      </p>
      <img src="../../assets/images/dynamic-operations.png" class="img-responsive"/>
      <p>
        Given the previously created dynamic Service, it is now possible to use the <code>/dynarest/Foo%20API/0.1/foo</code> endpoint (append after your Microcks base URL) to interact with it. This dynamic Service/API is indeed agnostic to a payload you send to it as long as it is formatted as JSON. For example, you can easily record a new <code>foo</code> resource having a <code>name</code> and a <code>bar</code> attributes like this: <br/><br/>

        <code>curl -X POST http://localhost:8080/dynarest/Foo%20API/0.1/foo -H 'Content-type: application/json' -d '{"name":"andrew", "bar": 223}'</code><br/>br/>

        And you should receive the following response :<br/><br/>
        <code>{ "name" : "andrew", "bar" : 223, "id" : "5a1eb52a710ffa9f0b7c6de8" }</code><br/><br/>

        What has simply done Microcks is recorded your JSON payload and assigned it an <code>id</code> attribute.
      </p>
    </section>

    <section id="dynamic-resources" class="article">
      <h2 class="arvo">Checking created resources</h2>

      <p>
        Creating resource is useful but how to check what are the already existing resources ? Let create another bunch of <code>foo</code> resources like this: <br/><br/>

        <code>curl -X POST http://localhost:8080/dynarest/Foo%20API/0.1/foo -H 'Content-type: application/json' -d '{"name":"andrew", "bar": 224}'</code><br/>
        <code>curl -X POST http://localhost:8080/dynarest/Foo%20API/0.1/foo -H 'Content-type: application/json' -d '{"name":"marina", "bar": 225}'</code><br/>
        <code>curl -X POST http://localhost:8080/dynarest/Foo%20API/0.1/foo -H 'Content-type: application/json' -d '{"name":"marina", "bar": 226}'</code><br/>

        <br/>
        Now, just hitting the <code>Resources</code> button just next to <code>Operations</code> section, you should be able to check all the resources Microcks has recorded as being viable representations of the <code>foo</code> resource. Each of them has received a unique identifier:
      </p>
      <img src="../../assets/images/dynamic-resources.png"/>
      <p>
        
      </p>
    </section>

    <section id="dynamic-dsl" class="article">
      <h2 class="arvo">Querying dynamic mock resources</h2>
      <p>
        <code>curl -X GET http://localhost:8080/dynarest/Foo%20API/0.1/foo/5a1eb52a710ffa9f0b7c6de8</code><br/><br/>

        <code>{ "name" : "andrew", "bar" : 223, "id" : "5a1eb52a710ffa9f0b7c6de8" }</code><br/><br/>
      </p>
      <p>
        <code>curl -X GET http://localhost:8080/dynarest/Foo%20API/0.1/foo -H 'Content-type: application/json' -d '{"name": "marina"}}'</code><br/><br/>

        <code>[{ "name" : "marina", "bar" : 225, "id" : "5a1eb608710ffa9f0b7c6deb" }, { "name" : "marina", "bar" : 226, "id" : "5a1eb613710ffa9f0b7c6dec" }]</code><br/><br/>
      </p>

      <p>
        <code>curl -X GET http://localhost:8080/dynarest/Foo%20API/0.1/foo -H 'Content-type: application/json' -d '{"bar": {$gt: 223, $lt: 226} }}'</code><br/><br/>

        <code>[{ "name" : "andrew", "bar" : 224, "id" : "5a1eb5fd710ffa9f0b7c6dea" }, { "name" : "marina", "bar" : 225, "id" : "5a1eb608710ffa9f0b7c6deb" }]</code><br/><br/>
      </p>
    </section>
  </div>
</div>
