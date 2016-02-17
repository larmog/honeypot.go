package = honeypot
default: all

keygen:
	@if [ ! -f rsa.key ]; then ssh-keygen -P "" -f rsa.key && rm rsa.key.pub; fi

get:
	go get -u golang.org/x/crypto/ssh
	go get -u golang.org/x/crypto/ssh/terminal

install:
	@go install -v .

all: format get install keygen build

run: format
	@go run -race $(package).go

build: test
	GOOS=linux GOARCH=arm GOARM=7 CGO_ENABLED=0 go build  -v $(package).go
	GOOS=linux GOARCH=arm GOARM=7 CGO_ENABLED=0 go build --ldflags '-extldflags "-static"' -o honeypot_static
	#go build -v $(package).go

format:
	go fmt *.go

.PHONY: all default install keygen format test
