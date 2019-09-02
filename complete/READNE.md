first
build with gradlew

then run this to build the docker images
gradlew docker

then use docker image ls to visualize the images

to run the docker images, for example:
docker run -it --rm -p 8080:8080 --name springboot fhillip/gs-multi-module-application

where:
-it means iteractive mode
--rm means that the container will autoremove itself after finishing the execution
-p 8080:8080 will use destinyPort:dockerImagePort
--name a custom name (which is optional) for the container instance
fhillip/gs-multi-module-application2 is the name of the image created


## Re-attach or Re-stablish connection
docker exec -it CONTAINER_ID CONTAINER_SCRIPT

for example:
docker exec springboot sh

this will exec the sh command at the docker container directory


## application2 Dockerfile
FROM openjdk:8-jdk-alpine
VOLUME /tmp
ARG DEPENDENCY=target/dependency
COPY ${DEPENDENCY}/BOOT-INF/lib /app/lib
COPY ${DEPENDENCY}/META-INF /app/META-INF
COPY ${DEPENDENCY}/BOOT-INF/classes /app
EXPOSE 8080
ENTRYPOINT ["java","-cp","app:app/lib/*","hello.app.DemoApplication"]


FROM is where the image will import from, in this case the image openjdk with the j8jdk pre instaled
VOLUME will mounth the /tmp directory (has to ivestigate a bit more)
ARG add a new argument or global variable in the Dockerfile to be used later, which is poiting to target/dependency
  target means the build forlder target
  /dependency is the directory dependency inside the build directory
COPY will copy centain folder to another folder so it can work when executed teh ENTRYPOINT command
EXPOSE this will expose to external the port 8080 for that container
ENTRYPOINT is the command that will be executed once the image is mounter to the contaienr
  this will run the java -cp with its arguments (read java -cp documentation for more information)


