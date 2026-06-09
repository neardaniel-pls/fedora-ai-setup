# Frequently Asked Questions

## General

### Which Fedora versions are supported?
Guides are tested on Fedora 42+. They should work on recent versions too.

### Do I need Docker?
No. The guides use Podman, which is the default container engine on Fedora. Podman is Docker-compatible and doesn't require a daemon.

### Do I need a GPU?
Not required. Ollama and Open Web UI work on CPU. GPU support (NVIDIA/AMD) is available for faster inference.

## Open Web UI

### What is Open Web UI?
A web-based chat interface for interacting with LLMs (like ChatGPT but self-hosted). It connects to Ollama for local model inference.

### Can I use models from Hugging Face?
Yes. The guide covers pulling models from Hugging Face and using them with Ollama.

### How do I update Open Web UI?
Pull the latest container image and restart:
```bash
podman pull ghcr.io/open-webui/open-webui:main
# Then restart the container
```

### How do I uninstall?
The guide includes complete uninstallation instructions for removing containers, images, and data.

## Troubleshooting

### Container won't start
- Check port 8080 isn't already in use: `sudo lsof -i :8080`
- View container logs: `podman logs <container-name>`
- Ensure Podman is running correctly: `podman info`

### Ollama not responding
- Check if Ollama is running: `systemctl status ollama`
- Verify Ollama is listening: `curl http://localhost:11434/api/tags`

### Out of memory
- Use smaller models (e.g., `phi`, `mistral` instead of `llama3:70b`)
- Close other applications
- Add swap space if needed

---

**Last Updated**: 2026-05-25
