############################
# STEP 1 build executable binary
############################
FROM golang:buster AS builder
# Install git.
# Git is required for fetching the dependencies.
RUN apt update && apt-get install git
WORKDIR $GOPATH/src/package/app/
COPY ./ ./
# Fetch dependencies.
# Using go get.
RUN go get -d -v ./... && \
    CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -a -installsuffix cgo -o /go/bin/main
############################
# STEP 2 build a small image
############################
FROM alpine
# Copy our static executable.
WORKDIR /app

COPY --from=builder /go/bin/main .

# Run the hello binary.

CMD ["./main"]