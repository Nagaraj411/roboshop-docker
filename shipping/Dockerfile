FROM maven
WORKDIR /opt/server
COPY pom.xml .
COPY src /opt/server/src
# copy src entries folder to the container
RUN mvn clean package
RUN mv /opt/server/target/shipping-1.0.jar /opt/server/shipping.jar
ENV CART_ENDPOINT="CART:8080" \
    DB_HOST="mysql"
CMD ["java", "-jar", "/opt/server/shipping.jar"]
