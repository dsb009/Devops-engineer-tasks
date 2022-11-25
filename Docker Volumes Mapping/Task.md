The Nautilus DevOps team is testing applications containerization, which issupposed to be migrated on docker container-based environments soon. In today's stand-up meeting one of the team members has been assigned a task to create and test a docker container with certain requirements. Below are more details:



a. On App Server 3 in Stratos DC pull nginx image (preferably latest tag but others should work too).

b. Create a new container with name media from the image you just pulled.

c. Map the host volume /opt/itadmin with container volume /tmp. There is an sample.txt file present on same server under /tmp; copy that file to /opt/itadmin. Also please keep the container in running state.

Solution:

1. Check for existing docker images : 
    docker images
2. Pull the latest nginx Image:
    docker pull nginx:latest
3. Copy the sample.txt to /opt/itadmin
    cp /tmp/sample.txt /opt/itadmin
4. docker run --name media -v /opt/itadmin: /tmp -d -it nginx:latest
# -v to map a directory on host to a folder in contianer 
# -d (detach mode) 
# The -it instructs Docker to allocate a pseudo-TTY connected to the container’s stdin; creating an interactive bash shell in the container. In the example, the bash shell is quit by entering exit 13. This exit code is passed on to the caller of docker run, and is recorded in the test container’s metadata. 
5. check for running container 
    docker ps
6. log in to the container using 
    docker exec -it <containerid> /bin/bash
7. check the location ll /var 