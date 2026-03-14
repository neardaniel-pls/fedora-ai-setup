# Guide: Open Web UI Installation with Podman

## 1. Overview

Open Web UI is a user-friendly and extensible web interface for various LLMs (Large Language Models). This guide will walk you through setting up the application in a containerized environment using Podman, which is the default container engine on modern Fedora systems.

The setup involves:
- Installing Podman
- Pulling the Open Web UI container image
- Running the container and making it accessible
- Installing Ollama to run models locally
- Pulling and running models from Hugging Face
- (Optional) Disabling Ollama autostart and managing it manually
- (Optional) Creating a systemd service for automatic startup

## 2. Dependencies

- **Podman**: The container engine used to run Open Web UI
- **`sudo`**: Required for system-level commands, including installing packages and managing systemd services

## 3. Installation & Setup

### Step 1: Install Podman

If you do not have Podman installed, open a terminal and run the following command:

```bash
sudo dnf install podman
```

**Verify the installation:**

```bash
podman --version
```

### Step 2: Pull the Open Web UI Image

Next, pull the official Open Web UI container image from a container registry. This command downloads the latest version.

```bash
podman pull ghcr.io/open-webui/open-webui:main
```

### Step 3: Run the Open Web UI Container

To run the application, you need to create a container from the image you just pulled. This command starts the container, maps the necessary port, and configures networking for local model access.

```bash
podman run -d \
  --network=host \
  -v open-webui:/app/backend/data \
  -e OLLAMA_BASE_URL=http://127.0.0.1:11434 \
  --name open-webui \
  --restart always \
  ghcr.io/open-webui/open-webui:main
```

**Command Breakdown:**
- `-d`: Runs the container in detached mode (in the background)
- `--network=host`: Uses the host's network namespace directly. This allows the container to access services on localhost (including Ollama at `127.0.0.1:11434`) without any network translation. **Note:** With host networking, port mapping (`-p`) is not needed—the container uses the host's ports directly
- `-v open-webui:/app/backend/data`: Creates a Podman volume named `open-webui` to persist application data. This is crucial for retaining your settings and chat history
- `-e OLLAMA_BASE_URL=http://127.0.0.1:11434`: Explicitly sets the Ollama API URL. With `--network=host`, the container can reach Ollama directly at `127.0.0.1:11434`
- `--name open-webui`: Assigns a memorable name to the container
- `--restart always`: Automatically restarts the container if it crashes or when the system reboots

> **Note for Fedora:** SELinux is enabled by default. Named volumes (used above) work automatically. If you later use bind mounts (e.g., `-v /home/user/data:/app/data`), append `:z` to the mount: `-v /home/user/data:/app/data:z`

**Verify the container is running:**

```bash
podman ps | grep open-webui
```

You should see output like:
```
<container_id>  ghcr.io/open-webui/open-webui:main  ...  0.0.0.0:8080->8080/tcp  open-webui
```

### Step 4: Access Open Web UI

Once the container is running, open your web browser and navigate to:

```
http://localhost:8080
```

You should see the Open Web UI interface, where you can create your first admin account.

### Step 5: Install Ollama for Local Models

To run LLMs locally, you need to install Ollama.

1. **Download and run the installer**:

```bash
curl -fsSL https://ollama.com/install.sh | sh
```

This command downloads and executes the official installation script.

2. **Verify the installation**:

```bash
ollama --version
sudo systemctl status ollama
```

After the script finishes, Ollama will be installed and the systemd service will be created. By default, the installer enables the Ollama service to start automatically on boot.

### Step 6: Disable Ollama Autostart (Optional)

If you only want to run Ollama when you need Open Web UI, you can disable the autostart behavior and stop the currently running service. This prevents Ollama from consuming resources when you're not using it.

**Disable autostart and stop immediately:**

```bash
sudo systemctl disable --now ollama
```

**Verify it's disabled and stopped:**

```bash
sudo systemctl status ollama
```

You should see `disabled` in the output and `inactive (dead)` for the active state.

### Step 7: Manage Ollama Manually

With autostart disabled, you can now start and stop Ollama as needed.

**Start Ollama:**

```bash
sudo systemctl start ollama
```

**Stop Ollama:**

```bash
sudo systemctl stop ollama
```

**Check Ollama status:**

```bash
sudo systemctl status ollama
```

**Restart Ollama:**

```bash
sudo systemctl restart ollama
```

### Step 8: Pull a Model from Hugging Face

With Ollama running, you can now pull models. To pull a GGUF model from Hugging Face, use the `ollama run` command with the `hf.co` prefix.

**Example:**

```bash
ollama run hf.co/unsloth/Qwen3-4B-Thinking-2507-GGUF:Q6_K
```

This command will download the specified model and start a chat session in your terminal. Once the model is downloaded, you can exit the terminal chat by typing `/bye`. The model is now available for Open Web UI to use.

**Note:** Model availability on Hugging Face may change over time. If the example model above is unavailable, search for GGUF models on [Hugging Face](https://huggingface.co/models?search=gguf) and use the appropriate `hf.co/username/model-name:quantization` format.

### Step 9: Connect Open Web UI to Ollama

Open Web UI should automatically detect your local Ollama instance. The container is configured with `--add-host=host.docker.internal:host-gateway`, which allows it to reach Ollama on your host machine.

1. Ensure Ollama is running: `sudo systemctl start ollama`
2. In the Open Web UI interface, click **"Select a model"**
3. You should see the model you just downloaded in the list
4. Select it to start chatting

If Open Web UI cannot find your Ollama instance, verify the connection from inside the container:

```bash
podman exec open-webui curl http://127.0.0.1:11434/api/tags
```

If this fails, ensure:
1. Ollama is running: `sudo systemctl start ollama`
2. The container was started with `--network=host`
3. The volume doesn't contain old cached settings (reset with `podman volume rm open-webui` if needed)

## 4. Managing the Container

Here are some useful commands for managing the `open-webui` container.

**Check container status:**

```bash
podman ps
```

*(Use `podman ps -a` to see all containers, including stopped ones)*

**View container logs:**

```bash
podman logs -f open-webui
```

*(The `-f` flag follows the log output in real-time)*

**Stop the container:**

```bash
podman stop open-webui
```

**Start the container:**

```bash
podman start open-webui
```

**Remove the container:**

*(You must stop the container before removing it)*

```bash
podman rm open-webui
```

## 5. Typical Workflow

If you've disabled Ollama autostart, here's a typical workflow for using Open Web UI:

1. **Start Ollama:**

```bash
sudo systemctl start ollama
```

2. **Start the Open Web UI container** (if not already running):

```bash
podman start open-webui
```

3. **Access Open Web UI** in your browser at `http://localhost:8080`

4. **When finished**, stop the services:

```bash
podman stop open-webui
sudo systemctl stop ollama
```

This prevents both services from consuming system resources when you're not actively using them.

## 6. Updating Open Web UI and Ollama

### 6.1 Backup Before Updating

**Backup Open Web UI:**

```bash
podman stop open-webui
mkdir -p ~/backups/open-webui
podman run --rm \
  -v open-webui:/data:ro \
  -v ~/backups/open-webui:/backup:z \
  alpine tar czf /backup/open-webui-backup-$(date +%Y%m%d-%H%M%S).tar.gz -C /data .
```

**Backup Ollama:**

```bash
sudo systemctl stop ollama
mkdir -p ~/backups/ollama
tar czf ~/backups/ollama/ollama-backup-$(date +%Y%m%d-%H%M%S).tar.gz ~/.ollama
sudo systemctl start ollama
```

> **Note**: Ollama models can be several GB. Ensure sufficient disk space.

### 6.2 Update Open Web UI

```bash
podman pull ghcr.io/open-webui/open-webui:main
podman stop open-webui
podman rm open-webui
podman run -d \
  --network=host \
  -v open-webui:/app/backend/data \
  -e OLLAMA_BASE_URL=http://127.0.0.1:11434 \
  --name open-webui \
  --restart always \
  ghcr.io/open-webui/open-webui:main
podman ps | grep open-webui
```

Access `http://localhost:8080` to verify your data is intact.

### 6.3 Update Ollama

```bash
sudo systemctl stop ollama
curl -fsSL https://ollama.com/install.sh | sh
sudo systemctl start ollama
ollama --version
ollama list
```

Models are preserved during the update.

### 6.4 Restore from Backup (if needed)

**Restore Open Web UI:**

```bash
podman stop open-webui
podman volume rm open-webui
podman volume create open-webui
podman run --rm \
  -v open-webui:/data \
  -v ~/backups/open-webui:/backup:ro \
  alpine sh -c "cd /data && tar xzf /backup/open-webui-backup-<timestamp>.tar.gz"
podman start open-webui
```

Replace `<timestamp>` with your backup file's timestamp.

**Restore Ollama:**

```bash
sudo systemctl stop ollama
mv ~/.ollama ~/.ollama.old
tar xzf ~/backups/ollama/ollama-backup-<timestamp>.tar.gz -C ~/
sudo systemctl start ollama
ollama list
rm -rf ~/.ollama.old
```

### 6.5 Best Practices

- Always backup before updating
- Check [Open Web UI](https://github.com/open-webui/open-webui/releases) and [Ollama](https://github.com/ollama/ollama/releases) release notes for breaking changes
- Update one component at a time and verify before proceeding
- Keep multiple recent backups
- Monitor disk space for backups and new images
- Schedule updates during downtime

## 7. Complete Uninstall

If you want to remove everything and start fresh, follow these steps carefully. This will remove Open Web UI, Ollama, all downloaded models, and associated configuration files.

### Remove Open Web UI Container and Volume

**Stop and remove the container:**

```bash
podman stop open-webui
podman rm open-webui
```

**Remove the Open Web UI volume** (this will delete all your Open Web UI data, conversations, and settings):

```bash
podman volume rm open-webui
```

**Remove the Open Web UI image** (optional, if you want to free up disk space):

```bash
podman image rm ghcr.io/open-webui/open-webui:main
```

### Remove Ollama

**Stop and disable the Ollama service:**

```bash
sudo systemctl stop ollama
sudo systemctl disable ollama
```

**Remove the Ollama systemd service file and reload systemd:**

```bash
sudo rm -f /etc/systemd/system/ollama.service
sudo systemctl daemon-reload
```

**Remove Ollama data directories** (this contains all downloaded models):

```bash
rm -rf ~/.ollama
sudo rm -rf /usr/share/ollama
```

**Remove the Ollama binary:**

```bash
sudo rm -f /usr/local/bin/ollama
```

**Remove Ollama user and group:**

```bash
sudo userdel -r ollama 2>/dev/null || sudo userdel ollama
sudo groupdel ollama 2>/dev/null || true
```

### Delete Individual Models (Without Uninstalling Ollama)

If you want to keep Ollama installed but only remove specific models:

**List all installed models:**

```bash
ollama list
```

**Remove a specific model:**

```bash
ollama rm <model_name>
```

**Example:**

```bash
ollama rm hf.co/unsloth/Qwen3-4B-Thinking-2507-GGUF:Q6_K
```

**Verify the model was deleted:**

```bash
ollama list
```

### Clean Up Podman (Optional)

After removing the Open Web UI container, you can optionally clean up unused Podman resources:

**Remove all stopped containers:**

```bash
podman system prune -f
```

**Remove all stopped containers and unused images:**

```bash
podman system prune -a -f
```

**Remove all stopped containers, unused images, and dangling volumes:**

```bash
podman system prune -a -f --volumes
```

### Verify Complete Removal

To confirm everything has been removed:

**Check for Ollama:**

```bash
which ollama
systemctl status ollama
```

Both should return "not found" or errors.

**Check for Open Web UI container:**

```bash
podman ps -a | grep open-webui
```

This should return nothing.

**Check for Podman volumes:**

```bash
podman volume ls | grep open-webui
```

This should return nothing.

**Check disk space to see what was freed:**

```bash
df -h
```

## 8. Troubleshooting

### "cannot connect to container" or "address already in use"

**Symptom**: The container fails to start, and logs show errors related to port conflicts.

**Solution**: Another service on your machine is likely using port 8080. You can identify what is using it with:

```bash
sudo lsof -i :8080
```

Either stop the conflicting service or modify the port mapping in your `podman run` command. For example, to use port 3000 instead:

```bash
podman stop open-webui
podman rm open-webui
podman run -d \
  --name open-webui \
  -p 3000:8080 \
  -v open-webui:/app/backend/data \
  --add-host=host.docker.internal:host-gateway \
  ghcr.io/open-webui/open-webui:main
```

Then access the UI at `http://localhost:3000`.

### Data is not persisting after restarts

**Symptom**: All settings and chat history are lost after restarting the container.

**Solution**: This usually means the volume was not correctly mounted. Ensure the `-v open-webui:/app/backend/data` part of your `podman run` command is present. You can inspect your container's configuration with:

```bash
podman inspect open-webui
```

Look for the **"Mounts"** section to verify the volume is attached.

### Open Web UI cannot connect to Ollama

**Symptom**: The model selection dropdown is empty, or you see connection errors like `Failed to fetch models` or `Connection refused to host.docker.internal:11434`.

**Root Cause**: Open Web UI stores connection settings in its database volume. If you previously configured settings in the UI, those override environment variables. Additionally, without `--network=host`, the container cannot reach `127.0.0.1:11434` on the host.

**Solution**:

1. First, verify that Ollama is running on the host:

```bash
sudo systemctl status ollama
curl http://127.0.0.1:11434/api/tags
```

2. Check if the container can reach Ollama:

```bash
podman exec open-webui curl http://127.0.0.1:11434/api/tags
```

3. If the above fails, you need to recreate the container with `--network=host`. **Important:** You must also remove the volume to clear any cached settings that might override your environment variable:

```bash
podman stop open-webui
podman rm open-webui
podman volume rm open-webui

podman run -d \
  --network=host \
  -v open-webui:/app/backend/data \
  -e OLLAMA_BASE_URL=http://127.0.0.1:11434 \
  --name open-webui \
  --restart always \
  ghcr.io/open-webui/open-webui:main
```

4. Verify the environment variable is set:

```bash
podman exec open-webui env | grep OLLAMA
```

This should output: `OLLAMA_BASE_URL=http://127.0.0.1:11434`

### Ollama service won't stop

**Symptom**: You try to stop Ollama with `systemctl stop ollama`, but it keeps restarting.

**Solution**: Make sure you haven't re-enabled autostart. Check the service status:

```bash
sudo systemctl is-enabled ollama
```

If it shows `enabled`, disable it:

```bash
sudo systemctl disable --now ollama
```

### Permission denied errors with volumes (Fedora/SELinux)

**Symptom**: The container starts but fails to write data, or you see "Permission denied" errors in logs.

**Solution**: This is typically an SELinux issue. Named volumes (used in this guide) should work automatically, but if you encounter issues, try:

1. **For named volumes**, relabel the volume:

```bash
podman volume inspect open-webui
# Note the mountPoint path, then:
sudo restorecon -R -v <mountPoint>
```

2. **For bind mounts**, always use the `:z` suffix:

```bash
-v /home/user/open-webui-data:/app/backend/data:z
```

### Container fails to start with "permission denied" on Fedora

**Symptom**: `podman run` fails immediately with permission-related errors.

**Solution**: This may be related to SELinux or user namespaces. Try:

```bash
# Check SELinux status
getenforce

# If Enforcing and causing issues, you can temporarily set to Permissive for testing
sudo setenforce 0

# Or better, ensure your system is updated and Podman is configured correctly
sudo dnf update podman
```

---

**Last Updated**: March 2026