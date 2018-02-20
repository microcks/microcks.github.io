---
layout: default
title: Using Microcks from Jenkins
---

<div class="content">
	<div class="jumbotron clearfix">
		<div class="container">
      <h1 class="page-title arvo">Automating Microcks tests with Jenkins</h1>
    </div>
	</div>
  <div class="container">
    <section id="jenkins-info" class="article">
      <h2 class="arvo">Microcks Jenkins plugin</h2>
      <p>
        Microcks provides a Jenkins plugin that you may find here: <a href="https://github.com/microcks/microcks-jenkins-plugin">microcks-jenkins-plugin</a>. This plugin allows your Jenkins builds and jobs to delegate the tests of microservices or API you just deployed to Microcks server. See <a href="../../using/tests/">this page on Tests</a> for more informations on running tests with Microcks.
      </p>
			<p>
				Using this plugin, it is really easy to integrate tests stages within your Continuous Integration / Deployment / Delivery pipeline. Microcks Jenkins plugin delegates tests realization and assertions checking to Microcks, wait for the end of tests or a configured timeout and just pursue or fail the current job depending on tests results.
			</p>

			<h3 class="arvo">Getting raw plugin</h3>
      <p>
        While not being distributed yet as an official Jenkins plugin, Microcks Jenkins plugin is available and can be downloaded from <a href="http://central.maven.org/maven2/io/github/microcks/microcks-jenkins-plugin/0.1.0/microcks-jenkins-plugin-0.1.0.hpi">Central Maven repository</a>. Just get the <a href="http://central.maven.org/maven2/io/github/microcks/microcks-jenkins-plugin/0.1.0/microcks-jenkins-plugin-0.1.0.hpi">HPI file</a> and install it on your Jenkins master <a href="https://jenkins.io/doc/book/managing/plugins/">your preferred way</a>.
      </p>

			<h3 class="arvo">Building an OpenShift Jenkins master embedding plugin</h3>
			<p>
				A common option for running Jenkins is through OpenShift platform. In that case, you may want to create your own custom Jenkins master container image embedding this plugin. While there's <a href="https://github.com/clerixmaxime/custom-jenkins">many ways of building such images</a>, as Microcks plugin is not yet an official Jenkins plugin, we provide our own OpenShift configuration for that.
			</p>
			<p>
				Given you have an OpenShift installation running and you're logged on it, just execute that command from terminal:<br/>
				<code>oc create -f https://raw.githubusercontent.com/microcks/microcks-jenkins-plugin/master/openshift-jenkins-master-bc.yml</code><br/>

				<br/>
				This should start a <code>Build</code> and then create an <code>ImageStream</code> called <code>microcks-jenkins-master</code> in your current project. After few minutes, a <code>microcks-jenkins-master:latest</code> container image should be available and you may be able to reference it as a bootstrap when creating a new Jenkins Service on OpenShift.
			</p>
    </section>

		<section id="usage" class="article">
			<h2 class="arvo">Using Microcks Jenkins plugin</h2>
			<p>
				Jenkins plugins may be used in 2 ways:<ul>
					<li>As a simple <code>Build Step</code> using a form to define what service to test,</li>
					<li>As an action defined using Domain Specific Language within a <code>Pipeline stage</code>.</li>
				</ul>
			</p>

			<h3 class="arvo">Simple build step usage</h3>
			<p>
				When defining a new project into Jenkins GUI, you may want to add a new <code>Launch Microcks Test Runner</code> step as shown in the capture below.<br/>
			</p>
			<img src="../../assets/images/jenkins-build-step.png" class="img-responsive"/>
			<p>
				The parameters that can be set here are:<ul>
					<li>The <code>API URL</code> of Microcks server: this is your running instance of Microcks where services or API are defined,</li>
					<li>The <code>Service Identifier</code> to launch tests for: this is simply a <code>service_name:service_version</code> expression,</li>
					<li>The <code>Test Endpoint</code> to test: this is a valid endpoint where your service or API implementation has been deployed,</li>
					<li>The <code>Runner Type</code> to use: this is the test strategy you may want to have regarding endpoint,</li>
					<li>The <code>Verbose</code> flag: allows to collect detailed logs on Microcks plugin execution,</li>
					<li>The <code>Timeout</code> configuration: allows you to override default timeout for this tests.</li>
				</ul>
			</p>

			<h3 class="arvo">DSL plugin usage</h3>
			<p>
				When defining a new CI/CD pipeline - even through the Jenkins or OpenShift GUI or through a <code>Jenkinsfile</code> within your source repository - you may want to add a specific <code>microcksTest</code> within your pipeline script as the example below:
			</p>
			<p>
				<pre><code>
node('maven') {
  stage ('build') {
    // ...
  }
  stage ('deployInDev') {
    // ...
  }
  stage ('testInDev') {
    // Add Microcks test here.
    microcksTest(apiURL: 'http://microcks-microcks.52.174.149.59.nip.io/api',
      serviceId: 'Beer Catalog API:0.9',
      testEndpoint: 'http://beer-catalog-impl-beer-catalog-dev.52.174.149.59.nip.io/api/',
      runnerType: 'POSTMAN', verbose: 'true')
  }
  stage ('promoteToProd') {
    // ...
  }
  stage ('deployToProd') {
    // ...
  }
}
				</code></pre>
			</p>
			<p>
				The parameters that can be set here are the same that in <code>Build Step</code> usage but take care to cases and typos:<ul>
					<li>The <code>apiURL</code> of Microcks server: this is your running instance of Microcks where services or API are defined,</li>
					<li>The <code>serviceId</code> to launch tests for: this is simply a <code>service_name:service_version</code> expression,</li>
					<li>The <code>testEndpoint</code> to test: this is a valid endpoint where your service or API implementation has been deployed,</li>
					<li>The <code>runnerType</code> to use: this is the test strategy you may want to have regarding endpoint,</li>
					<li>The <code>verbose</code> flag: allows to collect detailed logs on Microcks plugin execution,</li>
					<li>The <code>waitTime</code> configuration: allows you to override the default time quantity for this tests.</li>
					<li>The <code>waitUnit</code> configuration: allows you to override the default time unit for this tests (values in milli, sec or min).</li>
				</ul>
			</p>
			<p>
				Using Microcks and its Jenkins plugin, you may achieve some clean CI/CD pipelines that ensures your developed API implementation is fully aligned to expectations. See below a visualization of such a pipeline for our <code>Beer Catalog API</code> (full project to come soon).<br/>
			</p>
			<img src="../../assets/images/jenkins-pipeline-openshift.png" class="img-responsive"/>
		</section>
  </div>
</div>
