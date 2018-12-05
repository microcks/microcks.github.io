---
layout: default
title: Installing with docker-compose
---

<div class="content">
	<div class="jumbotron clearfix">
		<div class="container">
       <h2 class="page-title arvo">Installing with Docker-compose</h2>
    </div>
	</div>
  <div class="container">
    <section id="localhost" class="article">
      <h2 class="arvo">Localhost installation</h2>
      <p>
        For those of you familiar with simple Docker Compose, a <code>docker-compose</code> file is available within GitHub repository and can be used to rapidly test up things. First step is to clone the repository and then to execute docker-compose with local clone like in this commands :<br/><br/>
        <code>git clone https://github.com/microcks/microcks.git</code><br/>
        <code>cd microcks/install/docker-compose</code><br/>
        <code>docker-compose -f microcks.yml up -d</code><br/>

        <br/>
        After some minutes and components have been deployed, you should end up with a Spring-boot container, a MongoDB container, a Postman-runtime and a Keycloak container like in the trace below. The default user is <code>admin</code> with <code>123</code> password. The Microcks application is now available on <code>http://localhost:8080</code> URL.
        <pre><code>
$ docker ps
CONTAINER ID        IMAGE                                      COMMAND                  CREATED             STATUS              PORTS                    NAMES
6a563e9d87c1        microcks/microcks:latest                  "/bin/sh -c 'exec ..."   6 days ago          Up 33 seconds       0.0.0.0:8080->8080/tcp   microcks
162e99a97a6f        microcks/microcks-postman-runtime:latest   "node app.js"            6 days ago          Up 39 seconds       3000/tcp                 microcks-postman-runtime
b3cb4840597b        mongo:3.3.12                               "/entrypoint.sh mo..."   6 days ago          Up 39 seconds       27017/tcp                microcks-mongo
949e0b9bdac6        jboss/keycloak:3.4.0.Final                 "/opt/jboss/docker..."   6 days ago          Up 38 seconds       0.0.0.0:8180->8080/tcp   microcks-keycloak
        </code></pre>
      </p>
    </section>

    <section id="server" class="article">
      <h2 class="arvo">Server installation</h2>
      <p>
        When installing on a shared server that will be accessed from some other places and machines, you'll need to tweak some configuration files before launching the <code>docker-compose</code> command. The properties to setup/update in that case are the URL to access and redirect to Keycloak server and the access mode to Keycloak depending on the protocol your want to use.

        <br/>
        The directives just below show the detailed operations when using simple HTTP. If want to use HTTPS, you'll have to update the <code>sslRequired</code> and <code>keycloak.ssl-required</code> properties to <code>external</code> value.
        <pre><code>
$ hostname -f
  myserver.example.com
$ cd microcks/install/docker-compose/
$ cp keycloak-realm/microcks-realm-sample.json keycloak-realm/microcks-realm-sample.json.bak
$ apt-get install jq
$ jq '.applications |= map(if .name == "microcks-app-js" then .redirectUris = [ "http://myserver.example.com:8080/*" ] else . end) | .sslRequired |= "none"' keycloak-realm/microcks-realm-sample.json.bak > keycloak-realm/microcks-realm-sample.json
$ perl -i.bak -pe 's|KEYCLOAK_URL=http://localhost:8180/auth|KEYCLOAK_URL=http://myserver.example.com:8180/auth|' microcks.yml
$ perl -i.bak -pe 's|keycloak.ssl-required=external|keycloak.ssl-required=none|' config/application.properties
$ sudo docker-compose -f microcks.yml up -d
        </code></pre>
      </p>

      <p>
				All this directives are grouped into a single script named <code>setup-microcks-apt.sh</code> you'll find into the <code>install/docker-compose</code> directory. You can use it to setup your single server installation of Microcks. Just run the <code>docker-compose -f microcks.yml up -d</code><br/> command after having used this script.
      </p>
    </section>

    <section id="aws" class="article">
      <h2 class="arvo">Quick Azure installation</h2>

      <p>
        We provide this side project <a href="https://github.com/microcks/microcks-azure">microcks/microcks-azure</a> for easily setting up a demo server on Azure. This project reuse some form of the simple script exposed above, triggered by the Azure template instanciation.
      </p>
    </section>
  </div>
</div>
