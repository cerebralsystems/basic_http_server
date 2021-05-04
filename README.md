# Generate private key (.key)

## Key considerations for algorithm "RSA" >= 2048-bit

openssl genrsa -out server.key 2048

## Key considerations for algorithm "ECDSA" >= secp384r1

### List ECDSA the supported curves (openssl ecparam -list_curves)

openssl ecparam -genkey -name secp384r1 -out server.key

### Generation of self-signed(x509) public key (PEM-encodings .pem|.crt) based on the private (.key)

openssl req -new -x509 -sha256 -key server.key -out server.crt -days 3650

## Build or run

go build cerebral_http_server.go 
go build cerebral_https_server.go 

go run cerebral_http_server.go
go run cerebral_https_server.go

## Listening port

http:  9001
https: 9002

# httping
httping is a small program to request http server in order to print statuscode and the time to get the response.

Example :

$ httping -u https://www.github.com -s 500
connected to https://www.github.com, seq=1 time=761.159 bytes=206779 StatusCode=200
connected to https://www.github.com, seq=2 time=147.326 bytes=206779 StatusCode=200
connected to https://www.github.com, seq=3 time=143.971 bytes=206779 StatusCode=200
