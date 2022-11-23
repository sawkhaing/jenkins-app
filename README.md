
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
In Jenkinsfile create yaml template for require images.
Docker dind for docker build image "**docker:stable-dind**"
Helm for deploy builded app to the cluster "**alpine/helm:3.10.2**"
