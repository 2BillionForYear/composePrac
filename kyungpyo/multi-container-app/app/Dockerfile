ARG NODE_VERSION=19.5.0

## Base Image 설정
FROM node:${NODE_VERSION}-alpine

# Use production node environment by default.
# 왜? 불필요한 기능을 줄이기 위해
## 예를 들어, npm install 시 dev 환경에서는 개발 종속성을 제외하고 필요한 패키지만 설치됨
# 개발 종속성 : 테스트 프레임워크, 코드 품질 검사 도구 등 
ENV NODE_ENV production

WORKDIR /usr/src/app

# Download dependencies as a separate step to take advantage of Docker's caching.
# Leverage a cache mount to /root/.npm to speed up subsequent builds.
# Leverage a bind mounts to package.json and package-lock.json to avoid having to copy them into this layer.
# 복사 대신 두 파일을 컨테이너에 마운트하여 빌드 과정 더 빠름
# 캐시 마운트 : /root/.npm 디렉토리를 캐시로 설정
# 		npm이 이전에 다운로드한 패키지를 재사용 가능하여 빌드 과정이 더 빠름
# npm ci : package-lock.json에 명시된 정확 한 버전에 따라 종속성 설치

# 	   패키지 해상도 단계가 생략되어 npm install 보다 빠름
# --include=dev : 운영 및 개발 종속성 모두 설치 
RUN --mount=type=bind,source=package.json,target=package.json \
    --mount=type=bind,source=package-lock.json,target=package-lock.json \
    --mount=type=cache,target=/root/.npm \
    npm ci --include=dev

## 개발 중 파일 변경을 감지하고 자동으로 Node.js 애플리케이션을 재시작해주는 nodemon을 global로 설치
# install nodemon for hot-reloading
RUN npm install -g nodemon

# Copy the rest of the source files into the image.
COPY . .

## 모든 파일의 소유권을 node 사용자에게 넘기고, 실행 사용자를 node로 변경하여 보안 강화 
# Run the application as a non-root user.
# -R : 지정된 디렉토리의 모든 파일과 하위 디렉토리에도 동일한 명령을 적용
RUN chown -R node /usr/src/app
USER node

# Expose the port that the application listens on.
EXPOSE 3000

# Run the application in dev mode to use with Compose watch feature
# npm start : 운영, 배포 시 자동 재시작이나 파일 감시 없이 애플리케이션 실행
# npm run dev : 개발 중 실시간 코드 변경에 대응(compose file watch)
CMD npm run dev

