FROM golang:1.23-alpine AS build
WORKDIR /src
COPY ["main.go",  "."]
RUN CGO_ENABLED=0 go build -o server .

FROM alpine:3.21 as final
WORKDIR /app
COPY --from=build src/server .
ENTRYPOINT ["./server"]