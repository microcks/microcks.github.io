---
layout: default
title: OpenAPI usage for Microcks
---

<div class="content">
	<div class="jumbotron clearfix">
		<div class="container">
       <h1 class="page-title arvo">OpenAPI usage for Microcks</h1>
    </div>
	</div>
	<div class="container">
    <section id="intro" class="article">
			<h2 class="arvo">Overview</h2>

      <h3 class="arvo">Introduction</h3>
      <p>
        As <a href="https://www.openapis.org/">OpenAPI</a> emerges as an Open standard and provides way of defining <a href="https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.1.md#exampleObject">Example Objects</a>, Microcks has recently evolved to provide direct support for OpenAPI 3.0.
      </p>
      <p>
        With this new feature, you'll now be able to directly import your OpenAPI specification as a Job within Microcks. Then, it directly discover service definition as well as request/response samples defined as OpenAPI examples. If your specification embeds a JSON or OpenAPI schema definition for your custom datatypes, Microcks will use it for validating received response payload during <a href="../tests">tests</a> when using the <code>OPEN_API_SCHEMA</code> strategy.
      </p>
      <p>
        <blockquote>This feature may still be considered as <b>Experimental</b> within Microcks. We invite you to have a look and participate to related GitHub issues <a href="https://github.com/microcks/microcks/issues/24">#24</a> and <a href="https://github.com/microcks/microcks/issues/25">#25</a></blockquote>
      </p>

      <h3 class="arvo">Conventions</h3>
      <p>
        With OpenAPI <a href="https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.1.md#exampleObject">Example Objects</a>, you the ability to define named example fragments within your OpenAPI specification in YAML or JSON format. In order to produce working mocks, Microcks will need complete request/response samples. So to gather and aggregate fragments into something coherent, the importer will take care of collecting fragments having the same name and re-assemble them into comprehensive request/response pair.
      </p>
    </section>

    <section id="illustration" class="article">
      <h2 class="arvo">Illustration</h2>
      <p>
        We will illustrate how Microcks is using OpenAPI specification through a <code>Car API</code> sample. The specification file in YAML format can be found <a href="https://github.com/microcks/microcks/blob/master/src/test/resources/io/github/microcks/util/openapi/cars-openapi.yaml">here</a>. This API specification was designed using <a href="https://apicur.io">Apicurio</a>, a design studio that supports OpenAPI standards. It is a really simple API that allows registering cars to an owner, listing cars for this owner and adding passenger to a car.
      </p>

      <h3 class="arvo">Specifying request params</h3>

      <h3 class="arvo">Specifying response payload</h3>

      <p><pre><code>
responses:
  200:
    description: Success
    content:
      application/json:
        schema:
          type: array
          items:
            $ref: '#/components/schemas/Car'
        examples:
          laurent_cars:
            value: |-
              [
                  {"name": "307", "model": "Peugeot 307", "year": 2003},
                  {"name": "jean-pierre", "model": "Peugeot Traveller", "year": 2017}
              ]
      </code></pre></p>
      
    </section>
  </div>
</div>
