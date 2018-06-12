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
        With OpenAPI <a href="https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.1.md#exampleObject">Example Objects</a>, you are no able to define named example fragments within your OpenAPI specification in YAML or JSON format. In order to produce working mocks, Microcks will need complete request/response samples. So to gather and aggregate fragments into something coherent, the importer will take care of collecting fragments having the same name and re-assemble them into comprehensive request/response pair.
      </p>
    </section>

    <section id="illustration" class="article">
      <h2 class="arvo">Illustration</h2>
      <p>
        We will illustrate how Microcks is using OpenAPI specification through a <code>Car API</code> sample. The specification file in YAML format can be found <a href="https://github.com/microcks/microcks/blob/master/src/test/resources/io/github/microcks/util/openapi/cars-openapi.yaml">here</a>. This API specification was designed using <a href="https://apicur.io">Apicurio</a>, a design studio that supports OpenAPI standards. It is a really simple API that allows registering cars to an owner, listing cars for this owner and adding passenger to a car.
      </p>
      <p>
        Within this sample specification, we have defined 2 mocks - one for the registering operation and another for the listing cars operation:
        <ul>
          <li>The <code>POST /owner/{owner}/car</code> operation defines a sample called <code>laurent_307</code> where we'll register a Peugeot 307 for Laurent,</li>
          <li>The <code>GET /owner/{owner}/car</code> operation defines a sample called <code>laurent_cars</code> where we'll list the cars owned by Laurent.</li>
        </ul>
      </p>

      <h3 class="arvo">Specifying request params</h3>
      <p>
        Specifying request params encompasses path params, query params and header params. Within our 2 samples, we have to define the <code>owner</code> path param and using our convention introduced above, we have to define it 2 times - one for <code>laurent_307</code> mock and another for <code>laurent_cars</code> mock.        
      </p>

      <h4 class="arvo">Path parameters</h4>
      <p>
        This is done within the <code>parameters</code> part of corresponding API <code>path</code>, on <a href="https://github.com/microcks/microcks/blob/d183533c4129b2ecc1f5641107e7f6c0d43760f7/src/test/resources/io/github/microcks/util/openapi/cars-openapi.yaml#L83">line 83</a> of our file. Snippet is represented below:
        <pre><code>
parameters:
  - name: owner
    in: path
    description: Owner of the cars
    required: true
    schema:
      format: string
      type: string
    examples:
      laurent_cars:
        summary: Value for laurent related examples
        value: laurent
      laurent_307:
        $ref: '#/components/examples/param_laurent'
        </code></pre>
      </p>
      <p>
        One thing to notice here is that Microcks importer supports the use of references like <code>'#/components/examples/param_laurent'</code> to avoid duplication of complex values.
      </p>

      <h4 class="arvo">Query parameters</h4>
      <p>
        Query parameters are specified using parameters defined under the <code>verb</code> of the specification as you may find on <a href="https://github.com/microcks/microcks/blob/d183533c4129b2ecc1f5641107e7f6c0d43760f7/src/test/resources/io/github/microcks/util/openapi/cars-openapi.yaml#L20">line 20</a>. Snippet is represented below for the <code>laurent_cars</code> mock:
        <pre>code>
- name: limit
  in: query
  description: Number of result in page
  required: false
  schema:
    type: integer
  examples:
    laurent_cars:
      value: 20
        </code></pre>
      </p>

      <h3 class="arvo">Specifying request payload</h3>
      <p>
        Request payload is used within our <code>laurent_307</code> sample. It is specified under the <code>requestBody</code> of the specification as you may find starting on <a href="https://github.com/microcks/microcks/blob/d183533c4129b2ecc1f5641107e7f6c0d43760f7/src/test/resources/io/github/microcks/util/openapi/cars-openapi.yaml#L55">line 55</a>. Request payload may refer to OpenAPI schema definitions like in the snippet below:
        <pre>code>
requestBody:
  description: Car body
  content:
    application/json:
      schema:
        $ref: '#/components/schemas/Car'
      examples:
        laurent_307:
          summary: Creation of a valid car
          description: Should return 201
          value: '{"name": "307", "model": "Peugeot 307", "year": 2003}'
  required: true
        </code></pre>
      </p>

      <h3 class="arvo">Specifying response payload</h3>
      <p>
        Response payload is used within our <code>laurent_cars</code sample. It is defined under the <code>Http status</code> of the specification as you may find starting on <a href="https://github.com/microcks/microcks/blob/d183533c4129b2ecc1f5641107e7f6c0d43760f7/src/test/resources/io/github/microcks/util/openapi/cars-openapi.yaml#L40">line 40</a>. Response payload may refer to OpenAPI schema definitions like in the snippet below:
        <pre><code>
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
          </code></pre>
        </p>
        <p>
          And yes... I've called one of my car jean-pierre... ;-)
        </p>
    </section>

    <section id="Importing specification" class="article">
			<h2 class="arvo">Importing OpenAPI specification</h2>
			<p>
				When you're happy with your API design and example definitions just put the result YAML or JSON file into your favorite Source Configuration Management tool, grab the URL of the file corresponding to the branch you want to use and add it as a regular Job import into Microcks. On import, Microcks should detect that it's an OpenAPI specification file and choose the correct importer.
			</p>
      <p>
        Using the above <code>Car API</code> example, you should get the following results:
      </p>
      <img src="../../assets/images/openapi-mocks.png" class="img-responsive, center-block" style="max-width: 70%"/>
		</section>
  </div>
</div>
