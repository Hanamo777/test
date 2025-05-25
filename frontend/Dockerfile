# Stage 1: 빌드
FROM node:20-alpine as build

WORKDIR /app

# 의존성 파일 복사
COPY package.json ./

# Rollup 빌드를 위한 필수 도구 설치
RUN apk add --no-cache python3 make g++

# 모든 의존성 설치 (빌드에 필요한 devDependencies 포함)
RUN npm config set fetch-retries 5 && \
    npm config set fetch-retry-mintimeout 20000 && \
    npm config set fetch-retry-maxtimeout 120000 && \
    npm install --no-audit --no-optional && \
    npm rebuild rollup

# 소스 코드 복사
COPY . .

# 빌드
RUN npm run build

# Stage 2: 실행
FROM node:20-alpine

WORKDIR /usr/src/app

# 보안을 위한 non-root 사용자 생성
RUN addgroup -S appgroup && adduser -S appuser -G appgroup

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