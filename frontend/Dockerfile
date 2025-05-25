# Node.js 기반 이미지를 사용
FROM node:20-alpine

# 컨테이너 내부 작업 디렉토리 설정
WORKDIR /app

# package.json과 package-lock.json 복사
COPY package*.json ./

# 의존성 설치
RUN npm install

# 모든 소스 코드 복사
COPY . .

# Vite 서버에서 사용할 포트 설정
EXPOSE 5173

# 개발 서버 실행 명령어
CMD ["npm", "run", "dev"]
