FROM node:latest
RUN git clone https://github.com/kelleryvo/StreamDream.git ./app
RUN git checkout dev
WORKDIR /app
COPY package.json /app
COPY env.list /app
RUN npm install
COPY ./app /app
CMD node server.js
EXPOSE 8888
