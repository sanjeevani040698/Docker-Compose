# Docker-Compose

An application software, in general, is made up of many microservices which are, in large sense, independent of each other. So, building the whole application as a single unit is not considered a good practice due to many obvious reasons and are hence build independently.

These independent microservices need to be linked together when the application is deployed. One of the most preferrred way for this is docker-compose. It helps avoid the hassle of large and certain deprecated commands and provides an easier way of linking.

The procedure mainly requires a yaml file, apart from the application materials. This yaml file, docker-compose.yml, consists of various images, labeled under 'services' to be linked together along with their specifications.

Before starting, compose need to be installed using the commands:                                                               

sudo curl -L "https://github.com/docker/compose/releases/download/1.24.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

Then Apply executable permissions to the binary:                                                                          
sudo chmod +x /usr/local/bin/docker-compose

You can verify proper installation using                                                                                      
$ docker-compose --version

It should give something like                                                                                               
docker-compose version 1.24.0, build 1110ad01

Here is a simple example of linking a wordpress with mysql image.

We firstly pull the wordpress and mysql images from the docker hub using the commands:

docker pull wordpress                                                                                                       
docker pull mysql

This will download latest versions of both. 

# Yaml File

Now we need to put these images in the docker-compose.yml file as services. 

version: '3'  

services:                                                                                                                         
  wordpress:                                                                                                                              
    image: wordpress                                                                                                                
    ports:                                                                                                                            
      - 9080:80                                                                                                                               
    environment:                                                                                                                        
      WORDPRESS_DB_PASSWORD: abc123                                                                                                       


  mysql:                                                                                                                          
    image: mysql:latest                                                                                                               
    environment:                                                                                                                      
      MYSQL_ROOT_PASSWORD: abc123       
      
 
Note: Proper indentation needs to be ensured in the yaml file.

wordpress and mysql, under the services label, define the two services to be linked.

Below the service name, their attributes like image name and environment variables have been specified.

Giving the url localhost:9080 on the browser, should show the wordpress language page to start with.
