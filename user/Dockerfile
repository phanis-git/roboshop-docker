# FROM node:20
# WORKDIR /opt/server
# COPY package.json .
# COPY *.js .
# RUN npm install
# ENV MONGO="true" \
#     REDIS_UR="redis://redis:6379" \
#     MONGO_URL="mongodb://mongodb:27017/users"
# CMD ["node","server.js"]


# Below is the optimized image

FROM node:20.19.6-alpine3.22 AS build
WORKDIR /opt/server
# COPY package.json .
# COPY *.js .
COPY package.json . 
COPY *.js .
RUN npm install


FROM node:20.19.6-alpine3.22 
WORKDIR /opt/server
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop && \
    chown -R roboshop:roboshop /opt/server
EXPOSE 8080
LABEL project="roboshop" \
      component="user" \
      created_by="phani"  
ENV MONGO="true" \
    REDIS_UR="redis://redis:6379" \
    MONGO_URL="mongodb://mongodb:27017/users"
COPY --from=build /opt/server /opt/server
USER roboshop
# CMD ["node","server.js"]
CMD ["server.js"]
ENTRYPOINT ["node"]