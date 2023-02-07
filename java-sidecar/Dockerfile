# Extend vert.x image
FROM vertx/vertx4

# install open jdk
RUN apt-get --allow-releaseinfo-change -y update
RUN apt-get install -y software-properties-common
RUN apt-add-repository 'deb http://security.debian.org/debian-security stretch/updates main'
RUN apt-get --allow-releaseinfo-change -y update
RUN apt-get install -y openjdk-11-jre

#                                                       (1)
ENV JAVA_HOME /usr/lib/jvm/java-11-openjdk-amd64
ENV VERTICLE_NAME com.experiment.sidecar.MainVerticle
ENV VERTICLE_FILE build/distributions/java-sidecar-1.0.0-SNAPSHOT.tar
# Set the location of the verticles
ENV VERTICLE_HOME /experiment/app/java-sidecar


WORKDIR $VERTICLE_HOME

# Copy your verticle to the container                   (2)
COPY . ./

# RUN echo list $(ls -l ./build/distributions)
# RUN echo JAVA_HOME $JAVA_HOME

# For documentation
EXPOSE 8080

# Launch the verticle
ENTRYPOINT ["sh", "-c"]
CMD ["exec vertx run $VERTICLE_NAME -cp ./build/libs/*"]
