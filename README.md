
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

#### After deployed test the service
NOTE: It may take a few minutes for the LoadBalancer IP to be available.\
<pre><code>export SERVICE_IP=$(kubectl get svc --namespace app azt-app-azt-nginx --template "{{ range (index .status.loadBalancer.ingress 0) }}{{.}}{{ end }}")</code></pre>
<pre><code>echo http://$SERVICE_IP</code></pre>
![Screenshot 2022-11-23 at 5 52 28 PM](https://user-images.githubusercontent.com/12383368/203529241-28c5d2ec-acdb-4140-b7f6-5ee4a39c70e7.png)
