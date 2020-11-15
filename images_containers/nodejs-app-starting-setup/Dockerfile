FROM node:latest

WORKDIR /app

COPY package.json /app

RUN npm install

COPY . /app

# Expose é opcional, quando fazemos o port:port no run do docker, ele funciona mesmo sem o expose.
EXPOSE 80

CMD [ "node", "server.js" ]
