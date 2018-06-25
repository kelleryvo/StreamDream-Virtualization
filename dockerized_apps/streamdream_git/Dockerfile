FROM node:latest
RUN git clone https://github.com/kelleryvo/StreamDream.git
WORKDIR /StreamDream
RUN git checkout dev --
RUN npm install
CMD node server.js
EXPOSE 8888
