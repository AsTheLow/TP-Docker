# TP-Docker-Gautherot-Lantillon
We were unable to execute commands on a Windows environment, so we decided to switch to my work machine, which has an Ubuntu 22.04 OS and a Minikube installation, my test environment for my tutor project, as well as Len, which allows me to have a graphical interface of what I am doing
## The prerequisites to launch your assignment on Minikube are:

- Minikube
- Lens (to view the details of Minikube easily)
Please note that Lens is optional but recommended for a better experience.
- Kubectl (Optional) (https://github.com/AsTheLow/TP-Docker-Gautherot-Lantillon/blob/main/README.md#kubectl-configure-optional)

# Install Minikube
Firstly, you need to install Minikube (https://kubernetes.io/fr/docs/tasks/tools/install-minikube/).
Personally, my Minikube was installed using "installme", which is a YAML file created by my company. It is an application packaging and when launched, everything is installed at once.
Next, it is recommended to install Lens as it provides a simpler way to view the details of Minikube. You can create an account on Lens to be able to connect to it.

Once everything is installed, you can start Minikube by running the command <sup>"minikube start</sup>.

Once your Minikube is launched, you can then connect to Lens and access your Minikube interface, which should be empty except for some default files.

/!\ I use Minikube v1.27.0. I don't know if it makes any difference for the assignment.

# Minikube
To start your Minikube cluster, you can use the command "minikube start".
## Create namespace 
First, I will create a new namespace to avoid conflicts with my other namespaces in the project using the command 'kubectl create namespace tdgadrat'. The namespace name will be tdgadrat.
![image](https://user-images.githubusercontent.com/118971209/234888731-002f8ab6-4198-4693-b535-c9f6b2654379.png)
## Lens 
Now that you have successfully created your namespace, you can either use the command <sup>"kubectl get namespace tdgadrat"</sup> to verify its existence or connect to Lens for a graphical view. 
![image](https://user-images.githubusercontent.com/118971209/235267323-db296b8e-7d38-4afd-82b0-87d17cef6b33.png)
(To connect to Lens, simply click on "Mi".![image](https://user-images.githubusercontent.com/118971209/235267462-a24887c1-6f81-4a61-9200-d568f74b0253.png)
On Minikube, you can access Lens by navigating to "Workload" and then selecting "Overview". Lens should display your default namespace as well as any other namespaces that you have created.
![image](https://user-images.githubusercontent.com/118971209/235267534-9d5c3c49-2b64-48ef-9887-b4ac17c388b3.png)
## Deployments
Deployments on Minikube are used to manage the state and availability of containerized applications running on a Kubernetes cluster. Deployments provide a declarative way to define the desired state of a set of pods and ensure that the desired number of replicas are running at all times. Deployments also support rolling updates and rollbacks to ensure that application updates are deployed with minimal downtime and can be quickly rolled back if necessary.
To apply the "lamp-deployment.yaml" file to Minikube, you need to run the following command: <sup>"kubectl apply -f lamp-deployment.yaml -n tdgadrat"</sup> and <sup>kubectl get deployment -n tdgadrat</sup> for see if run :) 
![image](https://user-images.githubusercontent.com/118971209/235268236-d74948e8-6bc0-403c-ac2e-985fb21d4947.png)
You can see that the deployment has been successful on lens 
![image](https://user-images.githubusercontent.com/118971209/235268085-de2705d9-9605-498b-87ce-3d4dec17dc8b.png)

To summarize in my own words, a deployment is a file that is applied to create dependencies, such as multiple pods with one container per pod. In my case, the deployment includes containers for Apache, MySQL, and phpMyAdmin. If you want to remove these pods, you must delete the deployment first, because if a pod is killed, it is automatically recreated by the deployment.

![image](https://user-images.githubusercontent.com/118971209/235268997-10bceebe-9eb4-4aad-8957-bdb6c6b9a51e.png)

## PhpMyAdmin X MySql
Now that our containers are up and running and all showing green, we want to verify that our PhpMyAdmin is properly connected to our MySQL database.
![image](https://user-images.githubusercontent.com/118971209/235304196-435d2488-a852-4a35-9242-55770acb96ae.png) 
Pour vous connectez il vous suffit de cliquer sur le lien bleu la redirection est faite grâce automatiquement.
![image](https://user-images.githubusercontent.com/118971209/235304366-87a21530-5292-47e1-acfc-42fe6d855b98.png)
This redirection is created at the network level and port forwarding. Here, we can see that our redirection is active, which makes it easy to connect without much complexity. 
![image](https://user-images.githubusercontent.com/118971209/235304561-c5720343-e69b-4f1c-9f56-6fed99289b9d.png)
( Google def : Port forwarding is a feature that allows incoming network traffic to be redirected to a specific port on a Kubernetes node or container, to a local port on your machine.) 

Once on the PhpMyAdmin page, the login credentials are :
user : root 
password : password 
defined in the YAML file (also in the MySQL container)
![image](https://user-images.githubusercontent.com/118971209/235305351-a56c2882-7a7c-49f8-bb25-ae41a38731ea.png)
![image](https://user-images.githubusercontent.com/118971209/235305450-127b1efa-39cc-4042-b708-f8c267e7215e.png)
You are now connected and can see your SQL database!
![image](https://user-images.githubusercontent.com/118971209/235305594-313554fb-e6db-4dec-b7df-d82da09ff15d.png)

## Apache configuration 

Now that my Lamp infrastructure is up and running, I am not satisfied with the fact that my Apache page is not displaying anything.

![image](https://user-images.githubusercontent.com/118971209/235306676-7a8f62e0-0973-4184-860a-4dab27842a0d.png)

I will explain how I added the ConfigMap and made the necessary modifications in the Apache section of our deployment.

Firstly, I created a new YAML file for the ConfigMap. In this file, I specified the name and data to include. In our case, I added a key "index.html" with the HTML content that I wanted to display on the homepage of our website.

Next, I modified our deployment file to include a reference to this ConfigMap. I added a new volume "apache-config" with a reference to the ConfigMap that I just created. I also added a new volumeMount for our Apache container to mount the index.html file from this ConfigMap.

Once these modifications are made, our Apache deployment will be able to mount and display the HTML file from the ConfigMap we created, instead of using the default file that comes with the Apache image.

![image](https://user-images.githubusercontent.com/118971209/235309166-c312bbb4-3f38-4ce2-a895-cd11ceda3238.png)


### Additional information 


PHPMyAdmin is a popular and widely used MySQL database management tool in web development. It provides a user-friendly web interface to administer MySQL databases.

In the code you shared, the deployments of PHPMyAdmin and MySQL are connected together because PHPMyAdmin requires a MySQL database to store its data and configuration settings. The environment variable "PMA_HOST" is used to specify the name of the MySQL service that PHPMyAdmin will connect to. The MySQL service must be accessible from the same Kubernetes cluster for PHPMyAdmin to successfully connect to the MySQL database.

#### Detail on Lens and my container PhpMyAdmin
CPU: Shows the current CPU usage of the PhpMyAdmin container.
Memory: Shows the current memory usage of the PhpMyAdmin container.
Filesystem: Shows the current filesystem usage of the PhpMyAdmin container.
Metrics not available at the moment: Indicates that there are no metrics available for the container at the moment.
Status: Shows the current status of the container, which is "running" and "ready".
Last Status: Shows the last status of the container, which was "terminated" due to an error with an exit code of 255. It also displays the start and end times of the container.
Image: Shows the image used to create the container, which is "phpmyadmin/phpmyadmin".
ImagePullPolicy: Shows the policy used to pull the image, which is "Always".
Ports: Shows the exposed port of the container, which is "80/TCP".
Environment: Shows the environment variables used by the container, which are "MYSQL_ROOT_PASSWORD" set to "password", "PMA_HOST" set to "mysql-service", and "PMA_PORT" set to "3306".
Mounts: Shows the mounted volumes used by the container, which is "/var/run/secrets/kubernetes.io/serviceaccount" mounted from "kube-api-access-v64hb" with read-only permission.
Liveness: Shows the liveness probe configuration for the container, which is an HTTP GET request to "http://:80/delay=30s" with a timeout of 5 seconds and a period of 10 seconds. The probe will consider the container as healthy if it receives a success response code of 1, and will consider it as unhealthy if it receives a failure response code of 3.

# Waterloo Algorithmics

Welcome to my personal section where I share some of the fantasies I embarked on, which unfortunately resulted in failure. However, as a Japanese proverb says, "Failure teaches more than success."

## Trying to do everything on the same deployment and therefore on the same pod.
When I started the project, I attempted to do everything on the same deployment file and therefore on the same pod. However, I encountered an error. When my Apache and MySQL were started, the phpMyAdmin kept restarting in a loop and remained stuck in orange. After my Apache was killed, phpMyAdmin started, but the problem was reversed.

## Solution

My issue was due to the fact that phpMyAdmin uses port 80, just like Apache. Even if I exposed port 8080 on phpMyAdmin, its Docker image does not allow it to be configured on a port other than 80. Check out the phpMyAdmin documentation on Docker: https://hub.docker.com/r/phpmyadmin/phpmyadmin/.

Thus, it conflicted with Apache. After several hours of research, I abandoned the idea of trying to do everything on the same deployment and split them into three deployments.


# Annex 

## Kubectl configure (Optional)
I believe that kubectl is installed and configured by default, but I prefer to set it up just in case it's not, so that you don't have to spend time looking for it on your own.
kubectl is a command-line tool for managing Kubernetes clusters. It allows you to deploy, manage, and monitor containers and applications running on a Kubernetes cluster.
To connect to a Kubernetes cluster running on Minikube, you first need to start the cluster by running the "minikube start" command. Once the cluster is started, you can connect to it by running the "kubectl config use-context minikube" command.

![image](https://user-images.githubusercontent.com/118971209/235265034-456c0569-b0f8-4c5e-bd8c-6a40b7e107f8.png)

### Automatic deployment of Docker containers.
Firstly, we will use the command "docker run --name apache bitnami/apache:latest" to fetch the latest Bitnami image from Docker Hub. 
![image](https://user-images.githubusercontent.com/118971209/234866025-739ecf71-a57b-41e9-8455-f04b91441d9d.png)

Afterwards, we can see that the image has been added to our Docker Desktop environment, which is a graphical interface for Docker. This works in the same way as Lens, which allows us to visualize the operations of Minikube.

![image](https://user-images.githubusercontent.com/118971209/234866245-dcfa4ce9-1c22-4769-b96a-1fdc01ad28dd.png)
 
