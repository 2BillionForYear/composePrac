# Node.js 버전 19.5.0의 공식 이미지를 기반으로!
# -alpine 버전은 경량화된 이미지를 의미
FROM node:19.5.0-alpine

# 컨테이너 안에서 작업할 디렉토리를 설정
# 이 디렉토리는 컨테이너 내부에서 코드와 파일들이 저장되는 기본 경로가 된다
WORKDIR /usr/src/app

# 로컬의 package.json 파일을 컨테이너로 복사
# package.json 파일은 프로젝트의 의존성 목록을 가지고 있음
COPY package.json .

# Node.js의 패키지 매니저인 npm을 사용하여 필요한 패키지를 설치
RUN npm install

# 로컬 디렉토리의 모든 파일을 컨테이너의 현재 작업 디렉토리로 복사
COPY . .

# 애플리케이션이 사용할 포트를 노출
# EXPOSE : 컨테이너가 외부에 노출할 포트를 지정
EXPOSE 3000

# CMD : 컨테이너가 시작될 때 실행할 기본 명령어를 지정
# 개발자 모드로 애플리케이션 시작
CMD npm run dev
