# SSH Container

A customizable SSH-enabled container based on Ubuntu 22.04 that can be used for testing, development, and staging environments.

## Features

- Ubuntu 22.04 base image
- Configurable user creation with sudo privileges
- OpenSSH server pre-configured
- Python3 installed (can be removed if not needed)
- Customizable user ID

## Build Arguments

| Argument      | Default Value | Description               |
| ------------- | ------------- | ------------------------- |
| USERNAME      | admin         | The username to create    |
| USER_PASSWORD | admin         | The password for the user |
| USER_ID       | 1000          | The numeric user ID       |

## Usage

### Basic Build

```bash
docker build .
```

This will create a container with default credentials (username: admin, password: admin)

### Custom Build

```bash
docker build \
  --build-arg USERNAME=myuser \
  --build-arg USER_PASSWORD=mypassword \
  --build-arg USER_ID=1001 \
  .
```

### Using Docker Compose

```bash
docker compose up -d
```

This will create two containers with different users as specified in the compose.yaml file.

## Connecting to the Container

```bash
# For basic build with default port mapping (2222)
ssh admin@localhost -p 2222

# For custom builds, use the username you specified
ssh myuser@localhost -p 2222
```

## Security Notes

- Default credentials should be changed in production environments
- SSH host keys are generated during build
- The user has sudo privileges without password (customizable)
- StrictHostKeyChecking is disabled by default in the compose configuration

## Examples

### Using with Ansible

```yaml
# inventory.yml
all:
  hosts:
    node1:
      ansible_host: localhost
      ansible_port: 2222
      ansible_user: admin
      ansible_password: admin
```

### Using with SSH Config

```
# ~/.ssh/config
Host docker-ssh
    HostName localhost
    Port 2222
    User admin
```

## Customization

You can customize the image further by:

1. Adding additional packages in the Dockerfile
2. Modifying SSH configuration
3. Adding your own SSH keys
4. Changing the base image to another Ubuntu version or different distribution

## Contributing

Feel free to submit issues and enhancement requests!
