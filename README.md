This is a repo to use as a quickstart to start working with Spring Boot and deploying to the WildFly application server.  This uses the mvn build system and creates a .war file that can be deployed.  The code also contains a sample REST based service listening at /hello.

As an added bonus, this repo can also be deployed directly as a docker container using the WildFly S2I builder image on OpenShift 3 with the following command:

	oc new-app wildfly:10.0~https://github.com/gshipley/bootwildfly.git


What, you don't have OpenShift 3 yet? Fix that immediately: www.openshift.org/vm

---
```
node {
    stage 'Checkout'
    git branch: 'master', url: 'https://github.com/btihor/bootwildfly.git'   
    // Get the maven tool
    // ** NOTE: This 'M3' maven tool must be configured in the global configuration
    def mvnHome = tool 'M3'
    
    stage 'Build'
    sh "${mvnHome}/bin/mvn -f pom.xml clean install -DskipTests"
 
    stage 'Test'
    sh "${mvnHome}/bin/mvn -f pom.xml test"
}
```
---
