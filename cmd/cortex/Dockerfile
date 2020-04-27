FROM golang:1.13-alpine AS builder
COPY . /build
WORKDIR /build
RUN CGO_ENABLED=0 go build -ldflags "-extldflags \"-static\" -s -w" -tags netgo -o cortex ./cmd/cortex/main.go
RUN mv /build/cortex /

FROM alpine:3.8
RUN        apk add --no-cache ca-certificates
WORKDIR /
COPY --from=builder /cortex /cortex
ENTRYPOINT ["/cortex"]
