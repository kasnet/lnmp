from nginx:1.13.6-alpine
ENV TIME_ZONE Asiz/Shanghai
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/g' /etc/apk/repositories && \
    apk update && \
    apk add --no-cache tzdata  && \ 
   echo "${TIME_ZONE}" > /etc/timezone && \ 
   ln -sf /usr/share/zoneinfo/${TIME_ZONE} /etc/localtime 
COPY default.conf /etc/nginx/conf.d
EXPOSE 80
STOPSIGNAL SIGTERM
CMD ["nginx", "-g", "daemon off;"]
