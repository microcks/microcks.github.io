---
layout: default
title: Installing on OpenShift
---

<div class="content">
	<div class="jumbotron clearfix">
		<div class="container">
       <h2 class="page-title arvo">Installing on OpenShift</h2>
    </div>
	</div>
  <div class="container">
		<section id="openshift" class="article">
      <h2 class="arvo">Instructions</h2>
      <p>
				The easiest way of installing Microcks for production use in most secured conditions is to do it on OpenShift. OpenShift in version 3.6 or greater is required. It is assumed that you have some kind of OpenShift cluster instance running and available. This instance can take several forms depending on your environment and needs :
				<ul>
					<li>Full blown OpenShift cluster at your site, see how to <a href="https://docs.openshift.com/container-platform/3.3/install_config/index.html">Install OpenShift at your site</a>,</li>
					<li>Red Hat Container Development Kit on your laptop, see how to <a href="http://developers.redhat.com/products/cdk/get-started/">Get Started with CDK</a>,</li>
					<li>Lightweight Minishift on your laptop, see <a href="https://github.com/minishift/minishift">Minishift project page</a>.</li>
				</ul>

				<blockquote>
					When running on OpenShift, take care that you did not have the <code>anyuid</code> capability enabled. This prevents Microcks from using OpenShift internal Identity Provider. <code>anyuid</code> addon is enabled by default on Red Hat CDK. You may want to turn it off by executing <code>oc adm policy remove-scc-from-group anyuid system:authenticated</code> as this is a bad practice.
				</blockquote>

				Then you have to ensure that Microcks templates for OpenShift are added and available into your Cluster. Templates come in 2 flavors: ephemeral or persistent. In persistent mode, template will claim a persistent volume during instanciation, such a volume should be available to your team / project on OpenShift cluster. Add the templates, by using these commands :<br/>
				<code>oc create -f https://raw.githubusercontent.com/microcks/microcks/master/install/openshift/openshift-ephemeral-full-template.yml -n openshift</code><br/>
				<code>oc create -f https://raw.githubusercontent.com/microcks/microcks/master/install/openshift/openshift-persistent-full-template.yml -n openshift</code><br/>

				<br/>
				Once this is done can now create a new project and instanciate the template of your choice ; either using the OpenShift web console or the command line. You will need to fill up some parameters during creation such as:<ul>
				 	<li>the hostname for routes serving Microcks and embedded Keycloak (typically <code>component_name-project-app_domain</code>),</li>
					<li>the URL for joining OpenShift Master,</li>
					<li>a name for an OAuth Client that will be created apart the app creation.</li>
				</ul>
				Typically, you'll got this kind of commands for a local Minishift instance:<br/><br/>
				<code>oc new-project microcks --display-name="Microcks"</code><br/>
				<code>oc new-app --template=microcks-persistent --param=APP_ROUTE_HOSTNAME=microcks-microcks.192.168.99.100.nip.io --param=KEYCLOAK_ROUTE_HOSTNAME=keycloak-microcks.192.168.99.100.nip.io --param=OPENSHIFT_MASTER=https://192.168.99.100:8443 --param=OPENSHIFT_OAUTH_CLIENT_NAME=microcks-client</code><br/>

				<br/>
				After some minutes and components have been deployed, you should end up with a Spring-boot Pod, a MongoDB Pod, a Postman-runtime Pod, a Keycloak Pod and a PostgreSQL Pod like in the screenshot below.<br/>
			</p>
			<img src="../../assets/images/running-pods.png" class="img-responsive"/>
			<p>
				 Now you can retrieve the URL of the created route using <code>oc get routes</code> command and navigate to this URL to get started with Microcks. Depending on your environment, URL should be something like <code>http://microcks-microcks.192.168.99.100.nip.io</code>. By default, Microcks integrates with OpenShift identity provider through the use of Keycloak but you may configure some other providers later.
			</p>
    </section>
  </div>
</div>
