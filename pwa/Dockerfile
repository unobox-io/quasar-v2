ARG NODE_VERSION=16.17.1

# COMMON STAGE ---------------------------------------------------------------------------------------------------------
FROM node:${NODE_VERSION}-alpine AS unobox_pwa_common

ARG NODE_ENV=development
ENV NODE_ENV=${NODE_ENV}

ARG NODE_USER=root
ENV NODE_USER=${NODE_USER}

RUN apk update && apk upgrade && \
    apk add --no-cache bash openssh

USER node

RUN mkdir -p /home/node/app
RUN mkdir -p /home/node/app/node_modules

WORKDIR /home/node/app

COPY --chown=node:node ./package*.json ./
COPY --chown=node:node ./yarn.lock ./

RUN set -eux; \
	yarn install

RUN yarn global add @quasar/cli

COPY --chown=node:node . .

VOLUME /home/node/app/node_modules

RUN set -eux; \
  yarn build

CMD ["yarn", "test"]


# PORTAL NGINX ---------------------------------------------------------------------------------------------------------
FROM nginx:1.23.1-alpine AS unobox_pwa_prod

COPY docker/nginx/conf.d/default.conf /etc/nginx/conf.d/default.conf

WORKDIR /usr/src/client/build

COPY --from=unobox_pwa_common /home/node/app/dist/pwa ./
