# TP-Docker-Gautherot-Lantillon
## The prerequisites to launch your assignment on Minikube are:

- Minikube
- Lens (to view the details of Minikube easily)

Please note that Lens is optional but recommended for a better experience.

Firstly, you need to install Minikube (https://kubernetes.io/fr/docs/tasks/tools/install-minikube/).
Personally, my Minikube was installed using "installme", which is a YAML file created by my company. It is an application packaging and when launched, everything is installed at once.
Next, it is recommended to install Lens as it provides a simpler way to view the details of Minikube. You can create an account on Lens to be able to connect to it.

Once everything is installed, you can start Minikube by running the command <sup>"minikube start</sup>.

Once your Minikube is launched, you can then connect to Lens and access your Minikube interface, which should be empty except for some default files.

/!\ I use Minikube v1.27.0. I don't know if it makes any difference for the assignment.

## Automatic deployment of Docker containers.
Firstly, we will use the command "docker run --name apache bitnami/apache:latest" to fetch the latest Bitnami image from Docker Hub. 
![image](https://user-images.githubusercontent.com/118971209/234866025-739ecf71-a57b-41e9-8455-f04b91441d9d.png)

Afterwards, we can see that the image has been added to our Docker Desktop environment, which is a graphical interface for Docker. This works in the same way as Lens, which allows us to visualize the operations of Minikube.

![image](https://user-images.githubusercontent.com/118971209/234866245-dcfa4ce9-1c22-4769-b96a-1fdc01ad28dd.png)

We were unable to execute commands on a Windows environment, so we decided to switch to my work machine, which has an Ubuntu 22.04 OS and a Minikube installation, my test environment for my tutor project, as well as Len, which allows me to have a graphical interface of what I am doing

First, I will create a new namespace to avoid conflicts with my other namespaces in the project using the command 'kubectl create namespace tdgadrat'. The namespace name will be tdgadrat.
![image](https://user-images.githubusercontent.com/118971209/234888731-002f8ab6-4198-4693-b535-c9f6b2654379.png)



#Waterloo Algorithmics

Welcome to my personal section where I share some of the fantasies I embarked on, which unfortunately resulted in failure. However, as a Japanese proverb says, "Failure teaches more than success."

##Trying to do everything on the same deployment and therefore on the same pod.
When I started the project, I attempted to do everything on the same deployment file and therefore on the same pod. However, I encountered an error. When my Apache and MySQL were started, the phpMyAdmin kept restarting in a loop and remained stuck in orange. After my Apache was killed, phpMyAdmin started, but the problem was reversed.

##Solution

My issue was due to the fact that phpMyAdmin uses port 80, just like Apache. Even if I exposed port 8080 on phpMyAdmin, its Docker image does not allow it to be configured on a port other than 80. Check out the phpMyAdmin documentation on Docker: https://hub.docker.com/r/phpmyadmin/phpmyadmin/.

Thus, it conflicted with Apache. After several hours of research, I abandoned the idea of trying to do everything on the same deployment and split them into three deployments.
