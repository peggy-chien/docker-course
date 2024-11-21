# this is how we can define a specific argument to be used in our application
ARG NODE_VERSION=23.2.0

FROM node:${NODE_VERSION}-alpine

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 3000

CMD ["npm", "run", "dev"]