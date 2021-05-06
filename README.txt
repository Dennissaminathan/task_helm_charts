# task_helm_charts

#Environment details:

	Operating system used : Ubuntu 18.04.5 LTS
	minikube version: v1.15.1
	Driver used : docker

	Mysql:
  	Version : 5.6

	Webapp:
  	Node js

	Minikube:
	v1.15.1

	Kubectl:
	v1.19.4

	Helm:
	v3.4.1


Webapp:
	Webapp is built using basic nodejs which connects to mysql DB and populate required DB, Table and also data.
	Docker image of this webapp is pushed to my public docker repo ( samind/docker-web-app:3.0.6) 
	Latest tag for this application is 3.0.6

	GET is configured with /data context path to retirieve data.

Mysql:
       Mysql image is directly used for the deployment. No changes done in the image.

Minikube:
 	minikube is started with driver=docker
	Minikube is enabled with ingress addons

Installation instructions:
	Pre-requisite:
	1) Minikube should be up and running with required driver ( Ingress compatible)
	2) Helm should be installed.
Clone :
	Clone following repo https://github.com/Dennissaminathan/task_helm_charts.git 

Execution:
	Run command " helm install myapp myapp"
	It creates new namespace called helmsp and would deploy all the required objects.
K8s Objects:
	Mysql: PV  PVC, Statefulset, Service, pod
	Webapp: Deployment, pod, Service, Ingress, Secret, Config map.
Secrets: 
	DB credentials are masked using secrets and passed inside container as a ENV.

Test the deployment:
	Run command kubectl get ingress or minikube kubectl -- get ingress , Get the host name of the ingress (currently configurd as webapplication) and the IP of the ingress.
	update the name and ip in /etc/hosts file. (Something like this :172.168.10.3 webapplication)

	After the successful host file updation , App can be accessed using 
	curl webapplication/data (data is the contect for the data retrival)

	the string "Hello world" would be shown.


	

