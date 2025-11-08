# Fedora AI & LLM Setup Scripts

A collection of guides for setting up AI, machine learning, and LLM tools on Fedora Linux systems.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Fedora Version](https://img.shields.io/badge/Fedora-42%2B-blue.svg)](https://getfedora.org/)

## Overview

This repository contains comprehensive guides for deploying and managing AI/LLM tools on Fedora, including containerized applications, local model management, and web interfaces.

## Repository Structure

```
fedora-ai-setup/
├── setup/
│   └── open-web-ui-guide.md
├── README.md
└── LICENSE
```

## Contents

- **Container Management**: Podman setup for AI applications
- **Web Interfaces**: Open Web UI and similar browser-based tools
- **Local Models**: Ollama setup and management
- **Model Management**: Hugging Face integration and model pulling
- **AI Development**: Development environment setup for AI projects

## Getting Started

1. Clone the repository:
```bash
git clone https://github.com/neardaniel-pls/fedora-ai-setup.git
cd fedora-ai-setup
```

2. Choose a setup guide:
```bash
ls setup/
# Run your chosen guide
```

## Featured Guides

### Open Web UI with Podman
Complete guide for setting up Open Web UI in a containerized environment using Podman, with local Ollama integration for model management.

### Future Guides
Planned content for:
- Local AI development environments
- Model fine-tuning setups
- AI toolchain installation
- Performance optimization for LLM workloads

## Contributing

Contributions are welcome! Please focus on:
- Container and Podman automation
- AI/LLM tool integration
- Performance optimization for AI workloads
- Security best practices for AI deployments

## Support

- 🐛 [Report Bugs](https://github.com/neardaniel-pls/fedora-ai-setup/issues/new?template=bug_report.md)
- 💡 [Request Features](https://github.com/neardaniel-pls/fedora-ai-setup/issues/new?template=feature_request.md)

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

**Note**: This repository focuses specifically on AI/LLM tooling on Fedora. For general system administration tools, see the companion [fedora-system-setup](https://github.com/neardaniel-pls/fedora-system-setup) repository.

**Note**: For practical utility scripts for daily use, see the companion [fedora-user-scripts](https://github.com/neardaniel-pls/fedora-user-scripts) repository.