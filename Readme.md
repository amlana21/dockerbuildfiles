# DockerFiles to quickly get build environments for personal projects  

This is short and simple list of various Docker Files using which different personal build/work environments can be launched easily.  
To use the Dockerfiles below are the pre-requisites:  
* Docker installed in your local machine  
* If remote system is being used, make sure to install Docker first  
* And internet connection if the images are required to be pushed to a Registry  

Below are descriptions for each of the Dockerfiles and how to use them.  

## General Build Environment(build)  
This will launch a Docker container with common development components installed. This can be launched and used as build containers in Jenkins pipeline or just as a general build or execution container. Components installed:  
 * Maven  
 * GIT  
 * Open JDK  
 * Node JS 12.x  
 * Python 3.6  

There is a directory pre-created which can be used to volume mount local codefiles or folders to the container. If the code directory in the container is needed, please use the below command to run the container:  

 ```docker container run -itd -v /local/code:/home/codefiles --name mycontainer <image_name>```  

 <strong>Steps to use: </strong>  

 * Build the image using this command  
  ```docker build -t <username>/<image_name>:<tag> ./build```  
 * Run the Container:  
  ```docker container run -itd --name my container <username>/<image_name>:<tag>```  


## Flask Environment(build_flask)  
This will launch a docker container with Flask installed and will start the web server. To run a Flask App with this web server, volume mount the app location as below. Make sure the app file name is 'app.py'.  
 ```docker container run -itd -v /local/code:/home/flaskapp -p 5000:5000 --name mycontainer <image_name>:<tag>```  
Below are the components installed in the container:  
 * Python 3.6  
 * Flask  

 This also exposes 5000 port so the Flask app can be accessed as:  
  ```http://<server-ip>:5000```  

 <strong>Steps to use: </strong>  

 * Build the image using this command  
  ```docker build -t <username>/<image_name>:<tag> ./build_flask```  
 * Run the Container:  
  ```docker container run -itd -v /local/code:/home/flaskapp -p 5000:5000 --name my container <username>/<image_name>:<tag>```  

## NGINX Environment(build_nginx)  
This will launch a docker container with a basic installation of Nginx and the server will be accessible on port 80.To host web files, run the container as below
 ```docker container run -itd -v /local/files:/usr/share/nginx/html --name mycontainer <image_name>:<tag>```  
Below are the components installed in the container:  
 * Nginx 

 This also exposes 80 port so the web app can be accessed as:  
  ```http://<server-ip>:80```  

 <strong>Steps to use: </strong>  

 * Build the image using this command  
  ```docker build -t <username>/<image_name>:<tag> ./build_nginx```  
 * Run the Container:  
  ```docker container run -itd -v /local/files:/usr/share/nginx/html -p 80:80 --name my container <username>/<image_name>:<tag>```  

## NodeJS Environment(build_node)  
This will launch a docker container with NodeJS installed and an Express web server running on port 3000.To use this NoDeJS server:  
 ```docker container run -itd -v /local/files:/nodefiles/src/public --name mycontainer <image_name>:<tag>```  

To define a different app, modify the Dockerfile before building the image and modify this below line to copy files from different location:  
 ```COPY src /nodefiles```

Below are the components installed in the container:  
 * NodeJS  
 * Express 

 This also exposes 3000 port so the web app can be accessed as:  
  ```http://<server-ip>:3000```  

 <strong>Steps to use: </strong>  

 * Build the image using this command  
  ```docker build -t <username>/<image_name>:<tag> ./build_node```  
 * Run the Container:  
  ```docker container run -itd -v /local/files:/nodefiles/src/public -p 3000:3000 --name my container <username>/<image_name>:<tag>```  

## Tomcat Environment(ubuntu_tomcat)  
This will launch a docker container with Tomcat Server installed and running on port 8094.To launch the server:  
 ```docker container run -itd -p 80:8094 --name mycontainer <image_name>:<tag>```

The installed Tomcat uses default manager credentials. Which can be changed if needed, before building the image.  
  - <strong>User: </strong>mydevopsuser  
  - <strong>Password: </strong>devopstomcat1
  - Change this in the <em>tomcat-users.xml</em> file

P.S: Do not delete the <em>context.xml</em> file.  

Below are the components installed in the container:  
 * <strong>Base Image: </strong>ubuntu:16.04   
 * Tomcat 8  
 * Default JDK 

 This also exposes 8094 port so the web app can be accessed as(if below port is mapped while launching the container):  
  ```http://<server-ip>:80```  

 <strong>Steps to use: </strong>  

 * Build the image using this command  
  ```docker build -t <username>/<image_name>:<tag> ./ubuntu_tomcat```  
 * Run the Container:  
  ```docker container run -itd -p 80:8094 --name my container <username>/<image_name>:<tag>```  