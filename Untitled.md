## 🐳 Docker BuildKit: `--mount=type=cache` Explained

### Example

```Dockerfile
RUN --mount=type=cache,target=/var/cache/apt,sharing=locked \
    apt-get update && apt-get install -y curl