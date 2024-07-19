Nginx SSL certificate pre-compression patch updated.

1. **`ssl_certificate_compression`**
   - **Context:** `http`, `server`, `mail`, `stream`
   - **Syntax:** `ssl_certificate_compression on | off;`
   - **Default:** `off`
   - **Description:** This directive enables or disables SSL certificate compression. When enabled, the server will use the OpenSSL library's certificate compression feature to compress certificates before sending them to clients.

2. **`ssl_certificate_compression_max_uncompressed_size`**
   - **Context:** `http`, `server`, `mail`, `stream`
   - **Syntax:** `ssl_certificate_compression_max_uncompressed_size <size>;`
   - **Default:** `16M`
   - **Description:** This directive sets the maximum allowable size for an uncompressed certificate. If the uncompressed certificate size exceeds this limit, the server will reject the connection. The size must be specified in bytes, but can also be suffixed with `k` (kilobytes) or `M` (megabytes).

3. **`ssl_certificate_compression_max_memory_per_conn`**
   - **Context:** `http`, `server`, `mail`, `stream`
   - **Syntax:** `ssl_certificate_compression_max_memory_per_conn <size>;`
   - **Default:** `16M`
   - **Description:** This directive sets the maximum memory usage allowed per connection due to certificate compression. If the memory usage for certificate compression exceeds this limit, the server will reject the connection. The size must be specified in bytes, but can also be suffixed with `k` (kilobytes) or `M` (megabytes).

### Summary of New Directives/Options

1. **`ssl_certificate_compression`**
   - Enables or disables SSL certificate compression.
   - Default is `off`.

2. **`ssl_certificate_compression_max_uncompressed_size`**
   - Sets the maximum allowable uncompressed certificate size.
   - Default is `16M`.

3. **`ssl_certificate_compression_max_memory_per_conn`**
   - Sets the maximum memory usage allowed per connection for certificate compression.
   - Default is `16M`.

These directives give administrators the ability to control and limit the resource usage associated with Nginx SSL certificate pre-compression, ensuring that memory and certificate size limits are respected to avoid potential issues with resource exhaustion or performance degradation.

Example

```
    server {
        listen 443 ssl;
        server_name example.com;

        ssl_certificate /etc/ssl/certs/example.com.crt;
        ssl_certificate_key /etc/ssl/private/example.com.key;

        # Enable SSL certificate compression
        ssl_certificate_compression on;

        # Set maximum uncompressed size to 8MB
        ssl_certificate_compression_max_uncompressed_size 8M;

        # Set maximum memory usage per connection to 8MB
        ssl_certificate_compression_max_memory_per_conn 8M;

        location / {
            root /var/www/example.com;
            index index.html;
        }
    }
```