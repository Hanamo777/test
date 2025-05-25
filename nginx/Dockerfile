FROM nginx:alpine

# 기본 nginx 설정 파일 제거
RUN rm -f /etc/nginx/conf.d/default.conf

# 우리의 nginx 설정 파일 복사
COPY nginx.conf /etc/nginx/conf.d/default.conf

# SSL 인증서 디렉토리 생성
# RUN mkdir -p /etc/letsencrypt/live/sambungalaxy.o-r.kr

EXPOSE 80