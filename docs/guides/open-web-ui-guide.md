# Open Web UI Setup Guide

This guide is a reference to the main setup guide located at [`setup/open-web-ui-guide.md`](../../setup/open-web-ui-guide.md).

For complete step-by-step instructions, see the [main guide](../../setup/open-web-ui-guide.md).

## Quick Reference

### Install Podman
```bash
sudo dnf install podman
```

### Install Ollama
```bash
curl -fsSL https://ollama.com/install.sh | sh
```

### Run Open Web UI
```bash
podman run -d \
  --network=host \
  -v open-webui:/app/backend/data \
  -e OLLAMA_BASE_URL=http://127.0.0.1:11434 \
  --name open-webui \
  --restart always \
  ghcr.io/open-webui/open-webui:main
```

### Pull a Model
```bash
ollama run hf.co/unsloth/Qwen3-4B-Thinking-2507-GGUF:Q6_K
```

### Access
Open http://localhost:8080 in your browser.

## Full Guide

For the complete guide with troubleshooting, uninstallation, and advanced configuration, see [`setup/open-web-ui-guide.md`](../../setup/open-web-ui-guide.md).

---

[Back to Documentation](../README.md)
