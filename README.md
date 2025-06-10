# Mattermost Multi-Architecture Docker Images

This repository provides multi-architecture Docker images for [Mattermost](https://github.com/mattermost/mattermost), including ARM64 support.

## 🏗️ Supported Architectures

- **AMD64** (x86_64) - Standard servers and desktop environments
- **ARM64** (AArch64) - Apple Silicon, AWS Graviton, Raspberry Pi 4+, etc.

## 📦 Available Images

### Enterprise Edition
```

docker pull ghcr.io/supersunho/docker-mattermost/mattermost:latest-enterprise

```
### Team Edition
```

docker pull ghcr.io/supersunho/docker-mattermost/mattermost:latest-team

```

## 🚀 Quick Start

### Using Docker Run

**Enterprise Edition:**
```
docker run -d
  --name mattermost-enterprise
  -p 8065:8065
  ghcr.io/supersunho/docker-mattermost/mattermost:latest-enterprise
```

**Team Edition:**
```
docker run -d
  --name mattermost-team
  -p 8065:8065
  ghcr.io/supersunho/docker-mattermost/mattermost:latest-team
```

### Using Docker Compose
```
version: '3.8'

services:
  postgres:
  image: postgres:13-alpine
  environment:
    POSTGRES_DB: mattermost
    POSTGRES_USER: mmuser
    POSTGRES_PASSWORD: mmuser_password
  volumes:
    - postgres_data:/var/lib/postgresql/data

  mattermost:
    image: ghcr.io/supersunho/docker-mattermost/mattermost:latest-team
    ports:
      - "8065:8065"
    environment:
      MM_SQLSETTINGS_DRIVERNAME: postgres
      MM_SQLSETTINGS_DATASOURCE: "postgres://mmuser:mmuser_password@postgres:5432/mattermost?sslmode=disable&connect_timeout=10"
    depends_on:
      - postgres
    volumes:
      - mattermost_data:/mattermost/data
      - mattermost_logs:/mattermost/logs
      - mattermost_config:/mattermost/config

volumes:
  postgres_data:
  mattermost_data:
  mattermost_logs:
  mattermost_config:
```

## 📋 Edition Differences

- **Enterprise Edition**: Full feature set (commercial license required)
- **Team Edition**: Core features only (fully open source)

## 🔄 Automated Builds

This repository uses GitHub Actions to automatically:
- Monitor Mattermost releases
- Build multi-architecture images for both editions
- Publish to GitHub Container Registry
- Create GitHub releases with usage instructions

## 📝 Version Tags

Images are tagged with:
- `latest-enterprise` / `latest-team` - Latest stable version
- `vX.Y.Z-enterprise` / `vX.Y.Z-team` - Specific version tags

## 🔗 Links

- **Original Mattermost Repository**: [mattermost/mattermost](https://github.com/mattermost/mattermost)
- **Mattermost Documentation**: [docs.mattermost.com](https://docs.mattermost.com/)
- **Docker Images**: [GitHub Container Registry](https://github.com/supersunho/docker-mattermost/pkgs/container/mattermost)

## ⚖️ License

This project follows the same licensing as the original Mattermost project. The build scripts and workflows in this repository are provided under the MIT License.

## 🤝 Contributing

This is an automated build repository. If you encounter issues with Mattermost itself, please report them to the [official Mattermost repository](https://github.com/mattermost/mattermost/issues).

For build-related issues specific to this multi-architecture setup, feel free to open an issue in this repository.

---

**Note**: This is an unofficial build. For official support, please refer to the [Mattermost website](https://mattermost.com/).








