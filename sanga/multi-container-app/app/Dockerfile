#1 베이스 이미지 생성
FROM node:19.5.0-alpine
#ENV NODE_ENV production

#2 작업 디렉토리 설정
WORKDIR /usr/src/app

#3 package.json과 package-lock.json을 이미지에 복사
# package.json과 package-lock.json을 이미지에 복사하여 npm ci 를 실행하기 위한 준비
# 의존성 설치를 위한 필수 파일
#npm ci 명령어가 정상적으로 작동하게 함
COPY package.json package-lock.json ./

#4 npm ci 명령어를 실행하여 의존성 설치
#npm ci 명령어는 package-lock.json에 정의된 정확한 버전의 패키지 설치
# --include=dev 옵션은 개발환경에서 필요한 개발 의존성도 함께 설치

RUN npm ci --include=dev

#5 애플리케이션 코드 복사
COPY . .

#6 애플리케이션이 사용하는 포트를 노출
EXPOSE 3000

#7 컨테이너가 시작될 때 실행할 기본 명령어 지정
# Node.js 애플리케이션을 개발 모드로 실행
CMD npm run dev
