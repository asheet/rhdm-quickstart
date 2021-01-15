# Red Hat DM/PAM Docker Sample

This repo is an example of how bundle a rhpam/rhdm project with the red hat kie-server docker image.

This project was forked from https://github.com/juliaaano/rhdm-quickstart. Thank you to Juliano Mohr
for his examples.

## Get started
Please review these files to understand how it is working:
1. Dockerfile
2. docker-compose.yaml
3. rhdm-dependencies/pom.xml
4. rhdm-kjar/pom.xml
5. rhdm-kjar - ruleflow.bpmn
6. rhdm-kjar - rules.drl

### Requirements
Maven and Docker installed

### Build with Docker

Access to **registry.redhat.io** (docker login) is required to build the JBoss image.

```
docker build --file Dockerfile --tag dockersample/rhdm-jboss .
```


#### JBoss EAP with Docker

```
docker-compose up --detach --force-recreate rhdm-jboss
docker-compose logs --follow rhdm-jboss
```

### Check to see if Kie-server is up and running
username & password - **admin:admin**

The **docker-compose.yaml** file containers the kiecontainer id

To see the running containers:
In Postman - BasicAuth=admin:admin - GET
```
http://localhost:18080/services/rest/server/containers
```

To run the process and rules:
In Postman - BasicAuth=admin:admin - POST - body={}
```
http://localhost:18080/services/rest/server/containers/dockersample/processes/ruleflow/instances
```
