# Default HTTP Domains

This document defines the default HTTP domains available in MCP Policy files.

## Overview

The `defaults` keyword includes a commonly needed set of HTTP domains for typical development and API access scenarios. This provides a secure baseline that covers most common use cases while allowing administrators to add specific additional domains as needed.

### Included Domains

#### Package Registries
- `registry.npmjs.org` - Node.js packages
- `*.npmjs.com` - npm registry services
- `pypi.org` - Python packages
- `*.pypi.org` - Python package index services
- `files.pythonhosted.org` - Python package hosting
- `rubygems.org` - Ruby gems
- `*.rubygems.org` - RubyGems services
- `crates.io` - Rust crates
- `*.crates.io` - Crates.io services
- `static.crates.io` - Crates static content
- `index.crates.io` - Crates index
- `nuget.org` - NuGet packages (.NET)
- `*.nuget.org` - NuGet services
- `api.nuget.org` - NuGet API
- `repo.maven.apache.org` - Maven Central
- `repo1.maven.org` - Maven Central mirror
- `central.maven.org` - Maven Central
- `search.maven.org` - Maven search

#### Version Control Systems
- `github.com` - GitHub
- `*.github.com` - GitHub services
- `api.github.com` - GitHub API
- `raw.githubusercontent.com` - GitHub raw content
- `codeload.github.com` - GitHub code download
- `gitlab.com` - GitLab
- `*.gitlab.com` - GitLab services
- `bitbucket.org` - Bitbucket
- `*.bitbucket.org` - Bitbucket services
- `api.bitbucket.org` - Bitbucket API

#### Cloud Service Providers
- `*.amazonaws.com` - Amazon Web Services
- `s3.amazonaws.com` - AWS S3
- `*.s3.amazonaws.com` - Regional S3 endpoints
- `*.googleapis.com` - Google Cloud Platform APIs
- `storage.googleapis.com` - Google Cloud Storage
- `*.google.com` - Google services
- `*.azure.com` - Microsoft Azure
- `*.azurewebsites.net` - Azure Web Apps
- `*.blob.core.windows.net` - Azure Blob Storage
- `*.cloudflare.com` - Cloudflare services
- `cloudflare.com` - Cloudflare

#### Container Registries
- `docker.io` - Docker Hub
- `*.docker.io` - Docker Hub services
- `registry-1.docker.io` - Docker Hub registry
- `index.docker.io` - Docker Hub index
- `quay.io` - Red Hat Quay
- `*.quay.io` - Quay services
- `ghcr.io` - GitHub Container Registry
- `*.pkg.dev` - Google Artifact Registry
- `gcr.io` - Google Container Registry
- `*.gcr.io` - Regional GCR endpoints

#### AI and ML APIs
- `api.openai.com` - OpenAI API
- `*.openai.com` - OpenAI services
- `api.anthropic.com` - Anthropic API
- `*.anthropic.com` - Anthropic services
- `api.cohere.ai` - Cohere API
- `*.cohere.ai` - Cohere services

**Note**: This list focuses on the most commonly used AI/ML APIs in MCP server contexts. Additional providers may be included based on demonstrated usage patterns and community feedback.

#### Content Delivery Networks (CDNs)
- `cdn.jsdelivr.net` - jsDelivr CDN
- `*.jsdelivr.net` - jsDelivr services
- `unpkg.com` - UNPKG CDN
- `cdnjs.cloudflare.com` - Cloudflare CDN
- `*.fastly.net` - Fastly CDN
- `*.akamaized.net` - Akamai CDN
- `*.edgecastcdn.net` - Edgecast CDN

#### Documentation and Learning Resources
- `docs.rs` - Rust documentation
- `readthedocs.io` - Read the Docs
- `*.readthedocs.io` - Read the Docs projects
- `readthedocs.org` - Read the Docs
- `*.readthedocs.org` - Read the Docs projects

#### Build and CI/CD Services
- `circleci.com` - CircleCI
- `*.circleci.com` - CircleCI services
- `travis-ci.org` - Travis CI
- `*.travis-ci.org` - Travis CI services
- `*.travis-ci.com` - Travis CI services

## Usage

To use the default domains in your policy file:

```yaml
version: "1.0"
description: "Policy with default HTTP domains"
permissions:
  network:
    allow:
    - defaults: true
    - host: "internal.mycompany.com"
```

## Combining with Other Rules

The default domains can be combined with explicit host and CIDR rules:

```yaml
network:
  allow:
  - defaults: true
  - host: "*.company.internal"
  - cidr: "10.0.0.0/8"
  deny:
  - host: "blocked.example.com"
```

Deny rules take precedence, so you can block specific domains even if they're included in the defaults.

## Security Considerations

### Domain Vetting Criteria

Domains are included in the `common-http` defaults only if they meet all of the following criteria:

1. **Reputation**: Well-established services with a proven track record
2. **Security Practices**: Organizations with documented security practices and incident response
3. **Usage Frequency**: Commonly needed in typical MCP server development and deployment scenarios
4. **Trust**: Services operated by reputable organizations (established companies, foundations, or communities)
5. **Purpose**: Serve a clear, legitimate development or operational need

### Best Practices

- The default domain set is designed to be broadly useful while maintaining security
- All domains are well-known, reputable services
- Wildcards are used sparingly and only for trusted organizations with multiple subdomains
- Consider using deny rules to block specific subdomains if needed
- For production environments with stricter requirements, specify explicit domains instead of using defaults
- Review the complete domain list periodically to ensure it aligns with your security policies
