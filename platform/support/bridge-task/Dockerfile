FROM golang:1.23.4 AS builder
WORKDIR /app
# Copy the entire repo for the replace directive to work
COPY . .
WORKDIR /app/platform/support/bridge-task
RUN go mod download
ARG TARGETARCH
RUN CGO_ENABLED=0 GOOS=linux GOARCH=${TARGETARCH} go build -o main

FROM alpine
LABEL org.opencontainers.image.source=https://github.com/dan-hook/sst
WORKDIR /app
COPY --from=builder /app/platform/support/bridge-task/main /app/main
CMD ["/app/main"]
