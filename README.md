# Fedora AI & LLM Setup Scripts

A collection of guides for setting up AI, machine learning, and LLM tools on Fedora Linux systems.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Fedora Version](https://img.shields.io/badge/Fedora-42%2B-blue.svg)](https://getfedora.org/)

## Overview

This repository contains guides for deploying and managing AI/LLM tools on Fedora Linux systems. Currently, it focuses on containerized applications and web interfaces for interacting with large language models.

## Prerequisites

- **Fedora Linux**: This guide is tested on Fedora 42+ but should work on recent versions
- **Command Line Experience**: Basic familiarity with terminal commands
- **Sudo Access**: Required for installing packages and managing system services
- **Podman**: Default container engine on modern Fedora systems (installation instructions provided)

## Project Status

This is an active project that currently focuses on Open Web UI setup. Additional guides for other AI/LLM tools are planned for future releases. Contributions and suggestions are welcome!

## Contents

- **Open Web UI Setup**: Complete guide for setting up Open Web UI with Podman and Ollama integration

## Quick Start

For a quick setup of Open Web UI with local model support:

1. Install Podman: `sudo dnf install podman`
2. Follow the [Open Web UI Setup Guide](setup/open-web-ui-guide.md)
3. Access the web interface at `http://localhost:8080`

## Getting Started

Go to the [setup](setup/) directory and read the available guide. Each guide contains step-by-step instructions for setting up specific AI/LLM tools on Fedora.

If you prefer to work locally, you can clone the repository:
```bash
git clone https://github.com/neardaniel-pls/fedora-ai-setup.git
cd fedora-ai-setup
```

## Featured Guides

### Open Web UI with Podman
Complete guide for setting up Open Web UI in a containerized environment using Podman, with local Ollama integration for model management. This guide covers:
- Podman container setup and management
- Ollama installation and configuration
- Model pulling from Hugging Face
- Troubleshooting common issues
- Complete uninstallation instructions

### Future Guides
Planned content for:
- Additional AI/LLM web interfaces
- Model optimization and management
- Development environment setup for AI projects

## Documentation

### [Documentation Hub](docs/README.md)
Guides and references

### [Quick Start Guide](docs/QUICK_START.md)
Get Open Web UI running in 10 minutes

### [Guides](docs/guides/)
- [Open Web UI Guide](docs/guides/open-web-ui-guide.md) — Points to the full setup guide

### [FAQ](docs/FAQ.md)
Common questions and troubleshooting

### [Contributing Guide](CONTRIBUTING.md)
How to contribute

### [Changelog](CHANGELOG.md)
History of changes

## Support

- 🐛 [Report Bugs](https://github.com/neardaniel-pls/fedora-ai-setup/issues/new?template=bug_report.md)
- 💡 [Request Features](https://github.com/neardaniel-pls/fedora-ai-setup/issues/new?template=feature_request.md)

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## Related Projects

Check out these other companion projects:

- **[fedora-system-setup](https://github.com/neardaniel-pls/fedora-system-setup)**: Comprehensive post-installation guide for Fedora Linux systems with essential configurations, repositories, drivers, and applications

- **[fedora-user-scripts](https://github.com/neardaniel-pls/fedora-user-scripts)**: Collection of utility scripts optimized for Fedora Linux systems, focusing on system maintenance, security, and file management

- **[near-whisper](https://github.com/neardaniel-pls/near-whisper)**: Free and open source GUI for local Whisper audio transcription on Fedora Linux systems