FROM golang:1.14.9-alpine AS builder
COPY . /build
WORKDIR /build
RUN CGO_ENABLED=0 go build -ldflags "-extldflags \"-static\" -s -w" -tags netgo -o cortex ./cmd/cortex/main.go
RUN mv /build/cortex /

FROM alpine:3.12
RUN        apk add --no-cache ca-certificates
WORKDIR /
COPY --from=builder /cortex /cortex
ENTRYPOINT ["/cortex"]
