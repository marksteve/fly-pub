FROM golang:1.19-alpine
RUN apk add --no-cache git
WORKDIR /app
RUN git clone https://github.com/davecheney/pub.git /app
RUN go build
CMD ./pub auto-migrate --dsn $DSN && ./pub serve --log-http --dsn $DSN --addr 0.0.0.0:9999
