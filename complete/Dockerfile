FROM maven:3.6.0-jdk-8-alpine

WORKDIR /usr/src/app

# First copy only the pom file. This is the file with less change
COPY ./pom.xml .

# Download the package and make it cached in docker image
RUN mvn -B -f ./pom.xml -s /usr/share/maven/ref/settings-docker.xml dependency:go-offline

# Copy the actual code
COPY ./ .

# Then build the code
RUN mvn -B -f ./pom.xml -s /usr/share/maven/ref/settings-docker.xml package

ENTRYPOINT ["java","-jar","./target/gs-uploading-files-0.1.0.jar"]