# syntax=docker/dockerfile:1

ARG NODE_VERSION=19.5.0
FROM node:${NODE_VERSION}-alpine AS builder

WORKDIR /usr/src/app

COPY package.json package-lock.json ./

# NODE_ENV에 따라 의존성 설치
ARG NODE_ENV=production
RUN if [ "$NODE_ENV" = "production" ]; then npm ci --only=production; else npm ci; fi

COPY . .

FROM node:${NODE_VERSION}-alpine

ENV NODE_ENV production
WORKDIR /usr/src/app

COPY --from=builder /usr/src/app ./

RUN chown -R node /usr/src/app
USER node

EXPOSE 3000

CMD ["npm", "start"]
