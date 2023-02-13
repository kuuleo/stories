

REF Rails docs

The Redis adapter also supports SSL/TLS connections. The required SSL/TLS parameters can be passed in ssl_params key in the configuration yaml file.
```
production:
  adapter: redis
  url: rediss://10.10.3.153:tls_port
  channel_prefix: appname_production
  ssl_params: {
    ca_file: "/path/to/ca.crt"
  }
```
The options given to ssl_params are passed directly to the OpenSSL::SSL::SSLContext#set_params method and can be any valid attribute of the SSL context. Please refer to the OpenSSL::SSL::SSLContext documentation for other available attributes.


