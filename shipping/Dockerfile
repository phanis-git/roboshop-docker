# FROM maven:3.5
# EXPOSE 8080
# WORKDIR /opt/server
# COPY pom.xml .
# COPY src ./src
# RUN mvn clean package 
# RUN mv target/shipping-1.0.jar shipping.jar 
# ENV CART_ENDPOINT="cart:8080" \
#     DB_HOST="mysql"
#     CMD ["java", "-jar", "shipping.jar"]



# Below is the optimized image

FROM maven:3.5-alpine AS build
EXPOSE 8080
WORKDIR /opt/server
COPY pom.xml .
COPY src ./src
RUN mvn clean package 
RUN mv target/shipping-1.0.jar shipping.jar 

FROM maven:3.5-alpine AS build
WORKDIR /opt/server
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop && \
    chown -R roboshop:roboshop /opt/server
LABEL com.project="roboshop"
      component="shipping"
      created_by="phani"
EXPOSE 8080
ENV CART_ENDPOINT="cart:8080" \
    DB_HOST="mysql"
COPY --from=build /opt/server /opt/server
USER roboshop
CMD ["java", "-jar", "shipping.jar"]

