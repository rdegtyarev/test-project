FROM node as builder

RUN mkdir /app

WORKDIR /app

ADD vue-project/package.json /app/package.json
ADD vue-project/package-lock.json /app/package-lock.json

RUN npm i

ADD ./vue-project /app

RUN npm run build && rm -rf /app/node_modules

FROM nginx:latest

RUN mkdir /app
WORKDIR /app
COPY --from=builder /app/ /app

RUN mv /app/dist/* /app && rm -rf /app/dist

ADD demo.conf /etc/nginx/conf.d/default.conf
