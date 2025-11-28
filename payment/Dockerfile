# FROM python:3.9
# EXPOSE 8080
# WORKDIR /opt/server
# COPY payment.ini .
# COPY *.py .
# COPY requirements.txt .
# RUN pip3 install -r requirements.txt
# ENV CART_HOST="cart" \
#     CART_PORT="8080" \
#     USER_HOST="user" \
#     USER_PORT="8080" \
#     AMQP_HOST="rabbitmq" \
#     AMQP_USER="roboshop" \
#     AMQP_PASS="roboshop123"
# CMD ["uwsgi", "--ini", "payment.ini"]


# Below is the optimized image

# FROM python:3.9-alpine AS build
# EXPOSE 8080
# WORKDIR /opt/server
# COPY payment.ini .
# COPY *.py .
# COPY requirements.txt .
# RUN pip3 install -r requirements.txt


# FROM python:3.9-alpine 
# WORKDIR /opt/server
# EXPOSE 8080
# RUN addgroup -S roboshop && adduser -S roboshop -G roboshop && \
#     chown -R roboshop:roboshop /opt/server
# LABEL project="roboshop" \
#       component="payment" \
#       created_by="phani"  

# ENV CART_HOST="cart" \
#     CART_PORT="8080" \
#     USER_HOST="user" \
#     USER_PORT="8080" \
#     AMQP_HOST="rabbitmq" \
#     AMQP_USER="roboshop" \
#     AMQP_PASS="roboshop123"
# COPY --from=build /opt/server /opt/server
# USER roboshop
# CMD ["uwsgi", "--ini", "payment.ini"]



# chat gpt optimized

FROM python:3.9-alpine AS build
WORKDIR /opt/server
COPY requirements.txt .
RUN apk add --no-cache gcc musl-dev python3-dev linux-headers
RUN pip3 install --no-cache-dir -r requirements.txt
COPY payment.ini .
COPY *.py .

FROM python:3.9-alpine
WORKDIR /opt/server
EXPOSE 8080
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
COPY --from=build /opt/server /opt/server
RUN chown -R roboshop:roboshop /opt/server
LABEL project="roboshop" \
      component="payment" \
      created_by="phani"
ENV CART_HOST="cart" \
    CART_PORT="8080" \
    USER_HOST="user" \
    USER_PORT="8080" \
    AMQP_HOST="rabbitmq" \
    AMQP_USER="roboshop" \
    AMQP_PASS="roboshop123"
USER roboshop
CMD ["uwsgi", "--ini", "payment.ini"]
