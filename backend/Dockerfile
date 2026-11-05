FROM openjdk:17

ENV JAR_FILE=target/screen-recording-api.jar

ADD  $JAR_FILE app.jar

ENTRYPOINT ["java","-jar","/app.jar"]