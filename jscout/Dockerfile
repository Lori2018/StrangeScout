FROM alpine AS builder
WORKDIR /strangescout
RUN apk add --update nodejs nodejs-npm
COPY ./ ./
RUN npm install -g @angular/cli
RUN npm update --save
RUN ng build -prod

FROM joshix/caddy:latest
COPY Caddyfile /var/www/html
COPY --from=builder /strangescout/dist /srv
EXPOSE 80 443
VOLUME /.caddy/
ENTRYPOINT ["caddy", "-agree"]
