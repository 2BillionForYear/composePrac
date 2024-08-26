# 첫 번째 단계: 빌드
FROM node:${NODE_VERSION}-alpine as builder
WORKDIR /usr/src/app
COPY package*.json ./
RUN npm ci
COPY . .

# 두 번째 단계: 프로덕션
FROM node:${NODE_VERSION}-alpine
WORKDIR /usr/src/app
COPY --from=builder /usr/src/app .
EXPOSE 3000
CMD ["npm", "start"]
