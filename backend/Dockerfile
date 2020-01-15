FROM golang:alpine AS build-env
RUN apk --no-cache add build-base git bzr gcc

RUN git clone https://github.com/Zygimantass/beer $GOPATH/src/github.com/Zygimantass/beer

WORKDIR $GOPATH/src/github.com/Zygimantass/beer

RUN go mod download
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix nocgo -o /app .

FROM alpine 

WORKDIR /
COPY ./config.yml /config.yml
COPY --from=build-env /app /.
ENTRYPOINT ["./app", "serve"]
