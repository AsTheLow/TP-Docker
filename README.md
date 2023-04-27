# TP-Docker-Gautherot-Lantillon
## Déploiement automatique de conteneurs Docker
Firstly, we will use the command "docker run --name apache bitnami/apache:latest" to fetch the latest Bitnami image from Docker Hub. 
![image](https://user-images.githubusercontent.com/118971209/234866025-739ecf71-a57b-41e9-8455-f04b91441d9d.png)

Afterwards, we can see that the image has been added to our Docker Desktop environment, which is a graphical interface for Docker. This works in the same way as Lens, which allows us to visualize the operations of Minikube.

![image](https://user-images.githubusercontent.com/118971209/234866245-dcfa4ce9-1c22-4769-b96a-1fdc01ad28dd.png)

We were unable to execute commands on a Windows environment, so we decided to switch to my work machine, which has an Ubuntu 22.04 OS and a Minikube installation, my test environment for my tutor project, as well as Len, which allows me to have a graphical interface of what I am doing

First, I will create a new namespace to avoid conflicts with my other namespaces in the project using the command 'kubectl create namespace tdgadrat'. The namespace name will be tdgadrat.
![image](https://user-images.githubusercontent.com/118971209/234888731-002f8ab6-4198-4693-b535-c9f6b2654379.png)
