# Stage 1: 프론트엔드 애플리케이션 빌드 (Vite 프로젝트)
FROM node:20-alpine as build

WORKDIR /app

# 의존성 파일 복사 및 설치
COPY package.json ./
COPY package-lock.json ./ # 또는 yarn.lock 파일을 사용한다면 yarn.lock 복사

RUN npm install --frozen-lockfile

# 소스 코드 복사
COPY . .

# Vite 빌드 명령 실행 (기본적으로 'dist' 폴더에 결과물 생성)
RUN npm run build

# Stage 2: 빌드된 애플리케이션 서빙 (Node.js 기반 경량 서버)
FROM node:20-alpine

WORKDIR /usr/src/app

# 'serve' 패키지 전역 설치 (정적 파일 서빙용)
RUN npm install -g serve

# 빌드 스테이지에서 생성된 정적 파일 복사
COPY --from=build /app/dist ./

# Nginx upstream 설정(frontend:5173)과 일치하도록 포트 노출
EXPOSE 5173

# 'serve' 명령을 통해 정적 웹 서버 시작
CMD ["serve", "-s", ".", "-l", "5173"]