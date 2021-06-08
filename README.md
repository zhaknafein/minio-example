# minio-example
Example setup for a simple Minio S3 server.

Choose whatever distribution you like that supports Docker. Data is assumed to be located in 4 partitions mounted as `/data/minio/data{1..4}`.

In both `docker-compose.yaml` and `traefik.toml` files there are some placeholder variables to be changed:
* `minio_access_key`: access key for root user
* `minio_secret_key`: secret key for root user
* `public_hostname`: set your public hostname, used for Traefik Let's Encrypt certificate generation (eg. s3.mydomain.com)
* `jwt_secret`: Minio Console JWT secret, a random string at least 24 chars.
* `pbkdf_passphrase`: Minio Console PBKDF passphrase, a random string at least 24 chars.
* `pbkdf_salt`: Minio Console PBKDF salt, a random string at least 24 chars.
* `minio_console_access_key`: Minio Console access key for admin user
* `minio_console_secret_key`: Minio Console secret key for admin user
* `traefik_admin_username`: Traefik web interface admin username
* `traefik_admin_password`: Traefik web interface admin hashed password (can be generated with htpasswd)

Using this configuration you will get:
* Minio S3 service on port 9000 (no SSL!)
* Minio Console on port 9090 (no SSL!)
* Traefik on ports 80 (HTTP, redirects to 443), 443 (HTTPS, proxying to Minio S3) and 8080 (Traefik console and API)
