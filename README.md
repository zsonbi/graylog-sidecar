# Graylog-sidecar
This repo is for creating a graylog sidecar to collect logs from the services which are scattered all around.

### Variables
- LOGGER_IP=127.0.0.1 # optional if it is a standalone container isn't needed
- GRAYLOG_TOKEN=token_get_it_from_graylog_server # The token you get from the server under the sidecars menu
- GRAYLOG_SIDECAR_NAME=my-sidecar-123 # The name the sidecar will be displayed in the core (useful for streams as well)
- GRAYLOG_SERVER="http://example.graylog.server/api/" # The address of the graylog server

### Encryption
Generate the client's certificates on the core server, and then place them in the configs/graylog-certs (you can reuse them if you wish)

#### Self signed client cert generation
```
openssl genrsa -out client.key 2048
openssl req -sha512 -new -key client.key -out client.csr -config client.conf
openssl x509 -days 36500 -req -sha512 -in client.csr -CAserial serial -CA ca.crt -CAkey ca.key -out client.crt -extensions v3_req -extensions usr_cert  -extfile client.conf
```

