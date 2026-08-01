FROM nginx:1.27-alpine

LABEL maintainer="Agam Tyagi"
LABEL project="Automated DevOps Infrastructure"

COPY index.html /usr/share/nginx/html/

EXPOSE 80

HEALTHCHECK --interval=30s \
  --timeout=5s \
  --start-period=10s \
  --retries=3 \
  CMD wget --spider http://localhost:80|| exit 1

CMD ["nginx", "-g", "daemon off;"]
