# Silicon Valley Code Camp 2018
This is repository on Containers, Serverless and the Cloud, and how it all is connected together.
If you like it, give me a star ⭐️ !

During my workshop at the SVCC in San Jose in October I will go over the following examples:

- Serverless: https://console.bluemix.net/docs/openwhisk/deploy_templates.html#hello-world-template https://console.bluemix.net/docs/openwhisk/openwhisk_actions.html#openwhisk_actions
- PaaS: https://github.com/IBM-Cloud/todo-apps
- Containers: https://console.bluemix.net/docs/tutorials/scalable-webapp-kubernetes.html#scalable-web-application-on-kubernetes


## Serverless

This example shows how it is economical and easy to run a serverless based application on IBM Cloud:

- checkout the pricing: https://console.bluemix.net/openwhisk/learn/pricing - calculate the cost using the tool at the bottom of the page!
- follow steps to create the hello world example: https://console.bluemix.net/docs/openwhisk/deploy_templates.html#hello-world-template 
- use this link to create a service - https://console.bluemix.net/openwhisk/create

## PaaS - Cloud deployment of ToDo app

This example shows on how fast one could deploy a cloud (PaaS) managed ToDo app in one of the languages of choice.

### local deployment

- step one - clone the repo: `git clone git@github.com:IBM-Cloud/todo-apps.git`
- step two - choose your language - here we choose java: `cd todo-apps/java/bluemix-todo-app`
- step three - build the app and run it locally: `mvn -P run` - check it here: http://localhost:8080
- step four - bring it to the cloud - you would need an IBM Cloud account:

### cloud deployment

- connect local env to IBM Cloud api : `bluemix api https://api.ng.bluemix.net`
- login to your account: `bluemix login -u <your email> -o org_name -s space_name` (alternatively use SSO: `bluemix login -sso`)
- set up your Cloudfoundry env: `bluemix target --cf`
- push your app to the cloud `bluemix app push <name of your app> -p target/bluemix-todo-app.war -b java_buildpack` - after this command finishes you can access the app on the cloud - it doesn't persist the created documents - the persistency will be added in the next steps
- create a NoSQL db service: `bluemix cf create-service cloudantNoSQLDB Lite todo-couch-db`
- bind created db service with your app: `bluemix cf bind-service <name of your app> todo-couch-db`
- restage the app - now the app will pick the VCAP definition of the db and will use it to persist the documents between reruns of the application: `bluemix cf restage <name of your app>`

## Container deployment with Docker and Kubernetes

In order to deploy your service in the Kubernetes cluster use the following tutorial:

- https://console.bluemix.net/docs/tutorials/scalable-webapp-kubernetes.html#scalable-web-application-on-kubernetes

 Follow me on Twitter: @blumareks
