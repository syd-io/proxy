# Nginx Proxy Manager & Cloudflare DDNS

This repository contains a `docker-compose` configuration to set up Nginx Proxy Manager with Cloudflare Dynamic DNS (DDNS).

## Overview

- **Nginx Proxy Manager**: A simple and powerful reverse proxy solution with a web-based GUI.
- **Cloudflare DDNS**: Automatically updates your Cloudflare DNS records with your current IP address.

## Requirements

- Docker & Docker Compose installed on your system.
- A Cloudflare account with an API token that has DNS edit permissions.
- Environment variables set up for data storage and Cloudflare authentication.

## Installation

1. **Clone this repository:**
   ```sh
   git clone https://github.com/syd-io/proxy.git
   cd proxy
   ```

2. **Create a `.env` file** in the project root and set the following variables:
   ```ini
   FOLDER_FOR_DATA=/path/to/data
   FOLDER_FOR_LETSENCRYPT=/path/to/letsencrypt
   CLOUDFLARE_API_TOKEN=your_cloudflare_api_token
   DOMAINS=yourdomain.com
   ```

3. **Start the containers:**
   ```sh
   docker compose up -d
   ```

4. **Access Nginx Proxy Manager**:
   - Open a web browser and go to `http://your-server-ip:81`
   - Default login:
     - **Email:** admin@example.com
     - **Password:** changeme

5. **Configure Proxy Hosts and SSL**:
   - Add your domains and configure SSL certificates within the Nginx Proxy Manager UI.

## Healthcheck

The `docker-compose.yml` includes a health check for Nginx Proxy Manager:
```yaml
healthcheck:
  test:
    - CMD
    - /usr/bin/check-health
  interval: 10s
  timeout: 3s
```
This ensures the service remains operational.

## Security Considerations

- The Cloudflare DDNS container is run in **read-only** mode with dropped capabilities for enhanced security.
- Uses `security_opt: - no-new-privileges:true` to prevent privilege escalation.

## Contributing

Feel free to submit issues and pull requests to improve this setup!

## License

This project is licensed under the MIT License.
