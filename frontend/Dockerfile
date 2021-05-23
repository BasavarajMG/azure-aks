FROM node:10 AS ui-build
WORKDIR /app
COPY . ./
RUN  cd frontend && npm install && npm run build

FROM nginx:alpine
#!/bin/bash
COPY ./nginx/nginx.conf /etc/nginx/conf.d/configfile.template
RUN rm -rf /usr/share/nginx/html/*
COPY --from=ui-build /app/build /usr/share/nginx/html
ENV PORT 8080
ENV HOST 0.0.0.0
EXPOSE 8080
CMD sh -c "envsubst '\$PORT' < /etc/nginx/conf.d/configfile.template > /etc/nginx/conf.d/default.conf && nginx -g 'daemon off;'"