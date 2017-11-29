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
        Eventhough Microcks promotes a contract first approach
      </p>
      <img src="../../assets/images/dynamic-link.png" class="img-responsive"/>
      <p>

      </p>
      <img src="../../assets/images/dynamic-form.png" class="img-responsive"/>
      <p>

      </p>
      <img src="../../assets/images/dynamic-operations.png" class="img-responsive"/>
      <p>
        <code>curl -X POST http://localhost:8080/dynarest/Foo%20API/0.1/foo -H 'Content-type: application/json' -d '{"name":"andrew", "bar": 223}'</code><br/>br/>

        And you should receive the following response :<br/><br/>
        <code>{ "name" : "andrew", "bar" : 223, "id" : "5a1eb52a710ffa9f0b7c6de8" }</code>
      </p>
    </section>

    <section id="dynamic-resources" class="article">
      <h2 class="arvo">Checking created resources</h2>

      <p>
        <code>curl -X POST http://localhost:8080/dynarest/Foo%20API/0.1/foo -H 'Content-type: application/json' -d '{"name":"andrew", "bar": 224}'</code><br/>br/>
        <code>curl -X POST http://localhost:8080/dynarest/Foo%20API/0.1/foo -H 'Content-type: application/json' -d '{"name":"marina", "bar": 225}'</code><br/>br/>
        <code>curl -X POST http://localhost:8080/dynarest/Foo%20API/0.1/foo -H 'Content-type: application/json' -d '{"name":"marina", "bar": 226}'</code><br/>br/>
      </p>
      <img src="../../assets/images/dynamic-resources.png" class="img-responsive"/>
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
      <p>

      <p>
        <code>curl -X GET http://localhost:8080/dynarest/Foo%20API/0.1/foo -H 'Content-type: application/json' -d '{"bar": {$gt: 223, $lt: 226} }}'</code><br/><br/>

        <code>[{ "name" : "andrew", "bar" : 224, "id" : "5a1eb5fd710ffa9f0b7c6dea" }, { "name" : "marina", "bar" : 225, "id" : "5a1eb608710ffa9f0b7c6deb" }]</code><br/><br/>
      </p>
    </section>
  </div>
</div>
