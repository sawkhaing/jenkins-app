
# Build and Deploy

#### Prerequisite

- Create pipeline in jenkins UI

	- Add github project path
	- Add github pull request builder
	- Add SCM and Jenkinsfile path 

- Add github auth
	- To auth with github and jenkins
- Add docker credentials file - config.json
	- For image push to docker hub

#### Wrokflow
In Jenkinsfile create yaml template for require images.\
Docker dind for docker build image "**docker:stable-dind**"\
Helm for deploy builded app to the cluster "**alpine/helm:3.10.2**"

![aks jenkins drawio](https://user-images.githubusercontent.com/12383368/203516160-4f809774-9c18-4862-a049-bc371a14d679.png)
