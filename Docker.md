# Docker-Notes

| Docker Command | Description |
| --- | ----------- |
| docker build -t **Name-of-DockerFile**  | To generate a docker image based on a Dockerfile |
| docker run -p 8081:8080 **Name-of-Image** | To start a docker container based on a given image |
|docker image inspect **image-id** |To display detailed image information for a given image id |
|docker ps -a|To show all containers including running and stopped|
|docker container restart container-id|To restart one or more containers|
|docker container ls |To get list of all the containers|
|docker run -v **Target Location**:**Default Location** **Name of Container**|It will store the data outside the default location, hence even if the container is deleted, data will be stay there.|
|docker run -e **Env-variable** **Name of Container**|-e is used to specify the environment variable|
|docker run -d -e MYSQL_ROOT_PASSWORD=db_pass123 --name mysql-db mysql|here, name, env variable is being passed before running the container|
|docker exec **name or id of container** ps -eaf| it will run the process inside the container whose name has been defined and “ps” will show list of all the process running inside the container.|
|docker network ls|it is used find the list of all the networks|
|docker network create --driver bridge --subnet 182.18.0.1/24 --gateway 182.18.0.1 wp-mysql-network|Create a new network named wp-mysql-network using the bridge driver. Allocate subnet 182.18.0.1/24. Configure Gateway 182.18.0.1??|

![image](https://user-images.githubusercontent.com/38420375/186398946-0e577f9c-fc4b-4349-8eaf-ae23954b86e0.png)
Here the regular commands are being bundled into .yml file. Which can be made to run by using command “docker-compose up”.

![image](https://user-images.githubusercontent.com/38420375/186398973-1b622cbf-b469-4dfa-a852-4acb86abb063.png)
Since, we have got to build the app that we have created. Hence, we can use image instead we will have to replace it with build. 

![image](https://user-images.githubusercontent.com/38420375/186399074-7e32b9a4-0659-4945-b04d-2152ba2e440f.png)
Version 3, automatically creates the network. Hence, we need not to use –link anymore.

 ![image](https://user-images.githubusercontent.com/38420375/186399174-854f976c-704b-4df7-b21e-e941094bfabe.png)
Here, in order to make separation between frontend and backend. Networks are used. 

[docker.pdf](https://github.com/shivam005/Important-Notes/files/9433548/docker.pdf)



|||
|||
|||
|||
|||
|||
|||
|||
|||
|||
|||
|||
|||
|||
|||
|||
|||
|||
|||
|||
|||
|||
|||
|||
|||
|||
|||
|||
|||
|||
|||
|||
||| 
|||
|||
|||
|||

## Steps for pulling image to local docker registry"

1. Docker Desktop > Settings > Resources > Proxies 
 add "http://localhost:8082" in web server and secure webserver

 2. Docker Desktop > Settings > Docker Engine 

 add (It has insecure registries):  

 {
  "builder": {
    "gc": {
      "defaultKeepStorage": "20GB",
      "enabled": true
    }
  },
  "docker": {
    "insecure-registries": [
      "registry url"
    ]
  },
  "experimental": false,
  "features": {
    "buildkit": true
  }
}

3. port forward to 8082

 ssh <AD_ACCOUNT>@localhost -p2200 -L8082:localhost:80

4. sudo vi /etc/hosts
add below mentioned mapping in the hosts file

########## Artifactory ###########

<IP_ADDRESS> <REGISTRY_URL>

5. docker login -u <USER> <Registry_URL>

6. docker pull <IMAGE_URL>

 
###################################-Docker Process-#############################
1.on the SandBox go microservice pod-
2.make tar exluding log folder-
--tar -czvf not-listener.tar
3.return back to sanbox and create image using tar
--docker build -t image_name:version
4.push the image
--docker push image_name:version
5.when we put this image on another service so we need to perform this steps:-
  1. create image tar -
    --docker save -o not-listener.tar not-listener:1.4.0
  2. put tar on server and need to load the tar-
    --docker load < not-listener.tar
  3. after load image we need to push the image
docker save -o not-listener.tar not-listener:1.4.0                 |
docker load < not-listener.tar                                              |
docker push artifactory/not-listener:1.4.0
