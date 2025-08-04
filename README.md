# A specification for MCP Policy Files

This repository defines a specification for a policy format to be used by another application to enforce permission controls on Model Context Protocol (MCP) servers. It is written in YAML format. The policies control various aspects of a runtime environment, including:

- Storage Permissions: Controlling access (read, write) to specific file system URIs.
- Network Permissions: Restricting network access to specific hosts, host patterns, or CIDR blocks.
- Environment Variables: Defining which environment variables are allowed to be accessed.
- Docker Runtime Configuration: Specifying security-related settings for Docker containers, such as privilege levels and Linux capabilities.

## Policy Structure

Basic YAML format:

```yaml
version: "1.0"
description: "My policy"
permissions:
  storage:
    allow:
    - uri: "fs://work/agent/**"
      access: ["read", "write"]
  network:
    allow:
    - host: "api.example.com"
```

### Storage Permissions

```yaml
storage:
  allow:
    - uri: "fs://work/agent/**"
      access: ["read", "write"]
    - uri: "fs://work/temp/*"
      access: ["read"]
```

### Network Permissions

```yaml
network:
  allow:
    - host: "api.service.com"
    - host: "*.internal.com"
    - cidr: "10.0.0.0/8"
```

### Environment Variables

```yaml
environment:
  allow:
    - key: "PATH"
    - key: "HOME"
```

### Docker Runtime

```yaml
runtime:
  docker:
    security:
      privileged: false
      capabilities:
        drop: ["ALL"]
        add: ["NET_BIND_SERVICE"]
```

## Contributing

Please see [CONTRIBUTING.md][Contributing] for more information on how to contribute to this project.

## Trademarks

This project may contain trademarks or logos for projects, products, or services. Authorized use of Microsoft
trademarks or logos is subject to and must follow
[Microsoft's Trademark & Brand Guidelines](https://www.microsoft.com/legal/intellectualproperty/trademarks/usage/general).
Use of Microsoft trademarks or logos in modified versions of this project must not cause confusion or imply Microsoft sponsorship.
Any use of third-party trademarks or logos are subject to those third-party's policies.

[Contributing]: CONTRIBUTING.md
