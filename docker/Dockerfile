FROM node:11-alpine as node
LABEL maintainer="rkc7h@virginia.edu"
ARG BUILD_ENV
ENV APP_LOC /ithriv_web
RUN apk update && apk upgrade && \
    apk add --no-cache bash git openssh python3 python2
WORKDIR $APP_LOC
COPY package*.json ./
RUN npm install -g @angular/cli
RUN npm install
RUN npm install source-map-explorer --save-dev
COPY . .
RUN npm run "build_$BUILD_ENV"

FROM nginx:alpine
LABEL maintainer="rkc7h@virginia.edu"
ENV APP_LOC /ithriv_web
RUN rm -rf /usr/share/nginx/html/*
COPY --from=node $APP_LOC/dist /usr/share/nginx/html
COPY ./nginx_app.conf /etc/nginx/conf.d/default.conf
EXPOSE 4200
