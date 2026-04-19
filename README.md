## How Image Tags Are Generated

Each image is pushed with **two tags** on every successful run:

| Tag | Value | Purpose |
|-----|-------|---------|
| `latest` | always `latest` | Points to the most recent build from `main` |
| `<commit sha>` | unique identifer for each version  (e.g. `a3f9c12`) | Immutable, pinned to the exact commit |

This is handled by [`docker/metadata-action`](https://github.com/docker/metadata-action):




## 🏷️ Docker Image Tagging Strategy

Each image is tagged with:

* **latest**

  * Always points to the most recent build

* **commit SHA**

  * Unique identifier for each version

### Example:

```
student-record-backend:latest
student-record-backend:abc1234
```

---