# Build Stage
FROM openjdk:17-jdk-slim as builder
RUN apt-get update && apt-get install -y maven git

# Set Git configuration to increase timeout
RUN git config --global http.postBuffer 104857600  # Increase post buffer size to 100MB
RUN git config --global http.lowSpeedLimit 0       # Disable low-speed limit
RUN git config --global http.lowSpeedTime 999999   # Set low-speed time to a high value

# Use HTTPS for cloning the repository
RUN git clone https://github.com/Ammar-Abdelhady-ai/vprofile-project.git && \
    cd vprofile-project && \
    git checkout docker && \
    mvn install -DskipTests  # Skip tests

# Runtime Stage
FROM tomcat:9-jre17
LABEL "project"="Vprofile"
LABEL "Author"="Ammar"

RUN rm -rf /usr/local/tomcat/webapps/*
COPY --from=builder /vprofile-project/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080
CMD ["catalina.sh", "run"]