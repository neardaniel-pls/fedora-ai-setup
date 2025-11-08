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

## Support

- 🐛 [Report Bugs](https://github.com/neardaniel-pls/fedora-ai-setup/issues/new?template=bug_report.md)
- 💡 [Request Features](https://github.com/neardaniel-pls/fedora-ai-setup/issues/new?template=feature_request.md)

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

**Note**: This repository focuses specifically on AI/LLM tooling on Fedora. For general system administration tools, see the companion [fedora-system-setup](https://github.com/neardaniel-pls/fedora-system-setup) repository.

**Note**: For practical utility scripts for daily use, see the companion [fedora-user-scripts](https://github.com/neardaniel-pls/fedora-user-scripts) repository.