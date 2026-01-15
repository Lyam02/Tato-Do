FROM node:18-alpine

# Installing libvips-dev for sharp Compatibility
RUN apk update && apk add --no-cache build-base gcc autoconf automake zlib-dev libpng-dev nasm bash vips-dev git

ARG NODE_ENV=development
ENV NODE_ENV=${NODE_ENV}

WORKDIR /opt/
COPY package.json package-lock.json ./

# Supprimer le package-lock s'il existe et réinstaller
RUN rm -f package-lock.json
RUN npm install -g node-gyp
RUN npm config set fetch-retry-maxtimeout 600000 -g
RUN npm install

ENV PATH=/opt/node_modules/.bin:$PATH

WORKDIR /opt/app
COPY . .

# Supprimer node_modules s'il existe dans le projet
RUN rm -rf node_modules .cache build

RUN chown -R node:node /opt/app
USER node

EXPOSE 1337
CMD ["npm", "run", "develop"]
