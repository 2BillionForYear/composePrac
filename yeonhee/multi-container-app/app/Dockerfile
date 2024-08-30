ARG NODE_VERSION=19.5.0

# 노드 이미지를 사용하며 NODE_VERSION 변수를 통해 버전을 지정
# -alpine을 붙여서 알파인 리눅스 기반의 이미지를 사용
# as builder는 이 단계의 이름을 builder로 지정
FROM node:${NODE_VERSION}-alpine as builder

ENV NODE_ENV=production

WORKDIR /usr/src/app

# 호스트 파일을 이미지의 특정 경로로 복사
# ackage.json과 package-lock.json 파일을 현재 작업 디렉토리(./)로 복사
COPY package.json package-lock.json ./ 

# npm ci 명령어를 사용하여 package-lock.json에 정의된 의존성을 설치
# --include=dev 플래그를 통해 개발 의존성도 설치
RUN npm ci --include=dev

# nodemon은 코드 변경 시 자동으로 서버를 재시작해주는 도구
RUN npm install -g nodemon

COPY . .

# 3000포트 노출
EXPOSE 3000

# ---------------------------------------------------------

# 새로운 빌드 시작
FROM node:${NODE_VERSION}-alpine

WORKDIR /usr/src/app

# 이전 builder 스테이지에서 작업 디렉토리의 모든 파일을 현재 스테이지의 작업 디렉토리로 복사함
COPY --from=builder /usr/src/app .

# 디렉토리의 소유자를 node 사용자로 변경. 보안상의 이유로 권장한답니다 지피티가
RUN chown -R node /usr/src/app 

USER node

CMD ["npm", "run", "dev"]
