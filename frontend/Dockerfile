# Stage 1: 빌드
FROM node:20 as build 
# node:20-alpine 대신 node:20 사용

WORKDIR /app

# 의존성 파일 복사
COPY package.json ./

# Rollup 빌드를 위한 필수 도구 설치 (Debian 기반 이미지용)
RUN apt-get update && apt-get install -y python3 make g++ build-essential 
# 이 줄을 활성화했습니다.

# 모든 의존성 설치 (빌드에 필요한 devDependencies 포함)
# npm 오류 메시지에 따라 기존 node_modules와 package-lock.json을 먼저 제거
RUN rm -rf node_modules package-lock.json && \
    npm config set fetch-retries 5 && \
    npm config set fetch-retry-mintimeout 20000 && \
    npm config set fetch-retry-maxtimeout 120000 && \
    npm ci  && npm rebuild rollup 

# 소스 코드 복사
COPY . .

# 빌드
RUN npm run build

# Stage 2: 실행
FROM node:20 
# node:20-alpine 대신 node:20 사용

WORKDIR /usr/src/app

# 보안을 위한 non-root 사용자 생성 (Debian 기반 이미지용)
RUN groupadd -r appgroup && useradd -r -g appgroup appuser

# serve 패키지 설치
RUN npm install -g serve

# 빌드된 파일 복사
COPY --from=build /app/dist ./

# 권한 설정
RUN chown -R appuser:appgroup /usr/src/app

# non-root 사용자로 전환
USER appuser

EXPOSE 5173

CMD ["serve", "-s", ".", "-l", "5173"]