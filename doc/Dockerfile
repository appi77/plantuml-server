# Tomcat 10 + Java 17 기반 이미지
FROM tomcat:10-jdk17-temurin

# Tomcat 설정(server.xml) 복사 (한글깨짐 방지 등)
#COPY server.xml /usr/local/tomcat/conf/server.xml

# 기본 제공되는 ROOT 앱 제거 (불필요한 예제 제거)
RUN rm -rf /usr/local/tomcat/webapps/*

# 빌드한 plantuml.war 복사
COPY plantuml.war /usr/local/tomcat/webapps/plantuml.war

RUN apt-get update && \
    apt-get install -y fonts-nanum && \
    rm -rf /var/lib/apt/lists/* && \
    fc-cache -fv

EXPOSE 8080
