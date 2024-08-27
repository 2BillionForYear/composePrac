ARG VERSION=19.5.0

FROM node:${VERSION}-alpine AS builder
ENV NODE_ENV development
WORKDIR /usr/src/app
COPY package.json package-lock.json ./
RUN npm ci --include=dev
COPY . .

FROM node:${VERSION}-alpine
WORKDIR /usr/src/app
COPY --from=builder /usr/src/app /usr/src/app
EXPOSE 3000

CMD ["npm", "run", "dev"]
