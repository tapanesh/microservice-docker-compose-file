# Guide to start the miroservices application

# 1. Required tools: 
---------------------

Docker need to be installed in your local machine.

The latest docker version comes with docker compose. 

What is Docker Compose  ? 

Docker Compose is used to run multiple containers as a single service. 
For example, suppose you had an application which required NGNIX and MySQL, 
you could create one file which would start both the containers as a service without the need to start each one separately.

Validate both docker and docker-compose installed in your local machine or not by using the following commands :

# $ docker --version
Docker version 19.03.5, build 633a0ea

# $ docker-compose --version
docker-compose version 1.24.1, build 4667896b

# 2.Step By Step Details to run the microservices application 
-------------------------------------------------------------

# Step-1 : Clone the docker-compose.yml file to your local machine.

git clone https://github.com/tapanesh/microservice-docker-compose-file.git

# Step-2 : Go inside the cloned directory

cd microservice-docker-compose-file/

# Step-3 : Type the below command to run all the dockerized microservices applications and wait for few minutes until all the application starts-up

docker-compose up

# Step-4 :  Open a new terminal tap ( Command + N) and type the below command  to see all the dockerized 

# $ docker images

| REPOSITORY                   |  TAG            |     IMAGE ID        |    CREATED         |    SIZE | 
|:-------------:|:----------:|:----------:|:----------:|:-----------:|
| tapanesh/ws-eureka-discovery  |  1.0        |          c9cd1666ebfa   |      2 hours ago  |        157MB| 
| tapanesh/user-service          | 1.0         |         4f925977391b    |     2 hours ago    |      166MB| 
| tapanesh/task-service         |  1.0     |             ea6fe61ca8f0    |     2 hours ago     |     167MB| 
| tapanesh/comment-service |       1.0      |            61e0dad1870d     |    2 hours ago    |      170MB| 
| tapanesh/api-gateway          |  1.0       |           49df7edd35c6 |        2 hours ago    |      148MB| 

# Step-5 : Simillarlly type the below command to see in which port  all these dockeried microservices applications are running.

# $ docker ps 

| CONTAINER ID      |  IMAGE            |                  COMMAND            |      CREATED         |    STATUS             |  PORTS                           |   NAMES | 
|:------------------:|:---------:|:-----------:|:----------:|:-----------:|:--------:|:--------:|
|ba72a3e92004    |    tapanesh/task-service:1.0        |     "sh -c 'java -jar /t…"    |  11 minutes ago      |   Up 11 minutes      |    0.0.0.0:9998->9998/tcp       |         microservice-docker-compose-file_task-service_1  | 
  | b2f6322253d5      |     tapanesh/user-service:1.0        |     "sh -c 'java -jar /t…"    |  11 minutes ago    |     Up 11 minutes       |   0.0.0.0:9997->9997/tcp, 9998/tcp    |  microservice-docker-compose-file_user-service_1  | 
  | 052a5b501c1f       |    tapanesh/comment-service:1.0      |    "sh -c 'java -jar co…"   |   11 minutes ago    |     Up 11 minutes    |      0.0.0.0:9999->9999/tcp          |      microservice-docker-compose-file_comment-service_1  | 
  | 28eb4024e28b       |    tapanesh/api-gateway:1.0         |     "sh -c 'java -jar zu…"  |    11 minutes ago       |  Up 11 minutes      |    0.0.0.0:8765->8765/tcp, 9999/tcp   |   microservice-docker-compose-file_zuul-api-gateway_1  | 
  | 39971675f731          | tapanesh/ws-eureka-discovery:1.0     | "sh -c 'java -jar /t…"    |  11 minutes ago    |     Up 11 minutes      |    0.0.0.0:8761->8761/tcp         |       microservice-docker-compose-file_ws-eureka-discovery_1  | 


# Microservices Application List: 
|1.|  ws-eureka-discovery|
|:---:|:----:|
|2.| api-gateway|
|3. |comment-service|
|4.| user-service|
|5. |task-service|


# Accessing microservices endpoints without using the API Gateway 

# 1. Get all users from user-service 

e.g. http://localhost:9997/1

Note: Simillarly you can try to find other 2 users details by specifying the userId as '2' and '3'

# 2. Get all the comments from comment-service for a particular task 

e.g. http://localhost:9999/comments/task11

Note: Simillarly you can try to find other 2 hard coded task - 'task12'.

# 3. Get all the task and it's comments details from task-service.

e.g. http://localhost:9998/task11

Note: Simillarly you can try to find the task and comment details for 'task12'




# Accessing microservices endpoints with API Gateway 



# 1. Get all users from user-service 

e.g. http://localhost:8765/user-service/1

Note: Simillarly you can try to find other 2 users details by specifying the userId as '2' and '3'

# 2. Get all the comments from comment-service for a particular task 

e.g. http://localhost:8765/comment-service/comments/task11

Note: Simillarly you can try to find other 2 hard coded task - 'task12'.

# 3. Get all the task and it's comments details from task-service.

e.g. http://localhost:8765/task-service/task11

Note: Simillarly you can try to find the task and comment details for 'task12'

