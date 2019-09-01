first
build with gradlew

then run this to build the docker images
gradlew docker

then use docker image ls to visualize the images

to run the docker images, for example:
docker run -it --rm -p 8080:8080 --name springboot fhillip/gs-multi-module-application2

where:
-it means iteractive mode
--rm means that the container will autoremove itself after finishing the execution
-p 8080:8080 will use destinyPort:dockerImagePort
--name a custom name (which is optional) for the container instance
fhillip/gs-multi-module-application2 is the name of the image created
