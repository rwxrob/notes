## 🐳 Docker BuildKit: `--mount=type=cache` Explained

### Example

```Dockerfile
RUN --mount=type=cache,target=/var/cache/apt,sharing=locked \
    apt-get update && apt-get install -y curl
```

---

### 🧱 Breakdown

**`RUN --mount=...`**  
This syntax comes from **Docker BuildKit** and allows temporary mounts (like caches or secrets) during a single `RUN` instruction.

To use it, you must enable BuildKit:

```bash
DOCKER_BUILDKIT=1 docker build .
```

---

### 🧩 Mount Options

| Option                  | Description                                               |
|-------------------------|-----------------------------------------------------------|
| `type=cache`            | Use a persistent cache directory across builds            |
| `target=/var/cache/apt` | Inside the container, this is where `.deb` files go       |
| `sharing=locked`        | Prevents concurrent access issues in parallel builds      |

---

### ✅ Why It’s Useful

- Speeds up repeated builds
- Reuses downloaded APT packages (or other cacheable files)
- Reduces bandwidth and CI build time

---

### 🔐 `sharing=locked` Explained

If multiple builds run in parallel and share the same cache, `sharing=locked` prevents:
- Corrupted or partially-written cache files
- Race conditions in shared build agents

---

### 🧠 Summary

Use this pattern when installing packages in Docker:

```Dockerfile
RUN --mount=type=cache,target=/var/cache/apt,sharing=locked \
    apt-get update && apt-get install -y <your-packages>
```

This keeps your build efficient, clean, and CI-friendly.

---

### 🛠️ Related Use Cases

- Cache `~/.cache/pip` for Python
- Cache `/go/pkg/mod` for Go
- Cache `.npm` or `.pnpm-store` for Node.js

Let me know if you want a reusable template for multi-stage builds using this!
