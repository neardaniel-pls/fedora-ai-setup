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

### Pull a Model
```bash
ollama pull llama3
```

### Run Open Web UI
```bash
podman run -d -p 8080:8080 \
  --add-host=host.containers.internal:host-gateway \
  -v open-webui:/app/backend/data \
  --name open-webui \
  --restart always \
  ghcr.io/open-webui/open-webui:main
```

### Access
Open http://localhost:8080 in your browser.

## Full Guide

For the complete guide with troubleshooting, uninstallation, and advanced configuration, see [`setup/open-web-ui-guide.md`](../../setup/open-web-ui-guide.md).

---

[Back to Documentation](../README.md)
