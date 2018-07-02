FROM node:latest
WORKDIR /app
COPY ./app/package.json /app
RUN npm install
COPY env.list /app
COPY ./app /app
CMD node server.js
EXPOSE 8888
