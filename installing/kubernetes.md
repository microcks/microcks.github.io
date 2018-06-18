---
layout: default
title: Installing on Kubernetes
---

<div class="content">
	<div class="jumbotron clearfix">
		<div class="container">
       <h2 class="page-title arvo">Installing on Kubernetes</h2>
    </div>
	</div>
  <div class="container">
    <section id="kubernetes" class="article">
      <h2 class="arvo">Instructions</h2>
      <p>
        One easy way if installing Microcks is to do it on Kubernetes. Kubernetes in version 1.6 or greater is required. It is assumed that you have some kind of Kubernetes cluster up and running available. This can take several forms depending on your environment and needs :
        <ul>
          <li>Lightweight Minikube on your laptop, see <a href="https://github.com/kubernetes/minikube">Minikube project page</a>,</li>
          <li>Google Cloud Engine account in the cloud, see how to start a <a href="https://console.cloud.google.com/freetrial">Free trial</a>,</li>
          <li>Any other Kubernetes distribution provider.</li>
        </ul>

        We provide <a href="https://raw.githubusercontent.com/microcks/microcks/master/install/kubernetes/kubernetes-ephemeral-full.yml">basic Kubernetes manifest</a> for simple needs but also a <code>Chart</code> for using with <a href="https://helm.sh/">Helm</a> Packet Manager. This is definitely the preferred way of installing apps on Kubernetes.<br/>

        Just clone the GitHub repository, go to Helm directory and install the chart with these commands:<br/>
        <code>git clone https://github.com/microcks/microcks.git</code><br/>
        <code>cd microcks/install/kubernetes/helm</code><br/>
        <code>helm install ./microcks --name microcks --namespace=microcks</code><br/>

        <br/>
        After some minutes and components have been deployed, you should end up with a Spring-boot Pod, a MongoDB Pod, a Postman-runtime Pod, a Keycloak Pod and a PostgreSQL Pod like in the screenshot below.<br/>
      </p>
      <img src="../assets/images/running-pods-k8s.png" class="img-responsive"/>
      <p>
        Now you can retrieve the URL of the created ingress using <code>kubectl get ingress -n microcks</code>. Before starting playing with Microcks, you'll have to connect to Keycloak component in order to configure an identity provider or define some users for the Microcks realm (see <a href="http://www.keycloak.org/docs/latest/server_admin/index.html#user-management">Keycloak documentation</a>). Connection to Keycloak can be done using username and password stored into a <code>microcks-keycloak-config</code> secret created during setup.
      </p>
    </section>
  </div>
</div>
