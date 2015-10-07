---
layout: default
title: A communication and runtime tool for API mocks
---

<div class="content">
	<div class="jumbotron clearfix">
		<div class="container">
        <h2 class="arvo">The communication and runtime tool for your <span class="hl">Micro</span>-services Mo<span class="hl">cks</span></h2>
        <img class="illustration" src="assets/images/microcks-process.png">
    </div>
	</div>
	<div class="container">
    <section id="features">
      <div class="row feature-row">
        <div class="col-md-4">
          <i class="fa fa-users fa-4x feature-icon"></i>
          <span class="feature arvo">Business Friendly</span>
          <blockquote class="feature-text">Use the tool your business expert knows: SoapUI or whatever! No need to learn a new DSL or configuration syntax.</blockquote>
        </div>
        <div class="col-md-4">
          <i class="fa fa-refresh fa-4x feature-icon"></i>
          <span class="feature arvo">Continuous Integration</span>
          <blockquote class="feature-text">Integrate seemlessly in your continuous build or pipelines.</blockquote>
        </div>
        <div class="col-md-4">
          <i class="fa fa-rocket fa-4x feature-icon"></i>
          <span class="feature arvo">Scalable</span>
          <blockquote class="feature-text">Scale to hundreds of mocks, billions of hits on a single instance.</blockquote>
        </div>
      </div>
    </section>
    <section id="whatis" class="article">
      <h2 class="arvo">What's Microcks?</h2>

      <p>Microcks helps providers of API and micro-services to rapidly deliver :
        <ul>
          <li>A <strong>comprehensible vision of their API</strong>, exposing sample requests and responses as well as base functionnal rules (cases when API responds <code>A</code> or <code>B</code> or raises exceptions)</li>
          <li>A set of <strong>testing environments</strong> to allow API consumers or System Under Tests to use API even if implementation is not finished!</li>
          <li><strong>Contract testing plans</strong> of their API, allowing them to run, record and compare contract tests runned againts different environments.</li>
        </ul>
      </p>

      <p>When deploying API, micro-services or SOA practices at large scale, Microcks solves the problems of <strong>providing and sharing
      consistent documentation and mocks</strong> to the involved teams. It acts as a central repository and server that can be used for 
      browsing but also by your Continuous Integration builds or pipelines.</p>

      <p>Finally, Microcks does not impose a new configuration or Domain Specific Language to describe your mocks. It uses the contracts
      and provides <strong>binding with SoapUI</strong> (with some naming conventions). Your business expert describe requests and responses
      with the tool he knows, Microcks translates it and can do it repeatdely every time new mocks appears into your SCM.</p>
    </section>
	</div>
</div>