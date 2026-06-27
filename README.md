# aiOS

> The AI Appliance Operating System

Turn any computer with a GPU into a private AI server for your entire network.
Version: Draft 0.2
Status: Community Proposal - Pre-Alpha
License: MIT
Project Type: Open Source

---

## What is aiOS?
aiOS is a lightweight, purpose-built Linux distribution that transforms commodity hardware into a dedicated local AI inference appliance.
Plug in. Turn on. Your network has a private AI server.
No driver configuration. No command line required. No Docker knowledge needed. No cloud dependencies. Everything runs locally.

---

## The Problem aiOS Solves
Running local AI models today requires assembling multiple pieces manually. Here is what users currently face:
Operating System: Ubuntu Server is a 6GB+ download. It is a general-purpose OS with hundreds of irrelevant packages including printing services, audio stacks, Bluetooth daemons, and desktop components that have nothing to do with AI.
GPU Drivers: Installing NVIDIA or AMD drivers requires manual configuration. Users must deal with kernel headers, secure boot conflicts, and nouveau driver blacklisting. This step alone can take hours for someone unfamiliar with Linux.
Container Runtime: Docker must be installed separately, followed by the NVIDIA Container Toolkit for GPU passthrough. Each step introduces potential permission issues and configuration errors.
Inference Engine: Ollama, vLLM, or llama.cpp must be installed via command line. Users need to create systemd service files manually to ensure the engine starts on boot and survives crashes.
Web Interface: Open WebUI or similar dashboards require separate installation, reverse proxy configuration, SSL certificate setup, and port management. This is complex even for experienced developers.
Network Access: Firewall rules must be manually configured. CORS settings need adjustment. Static IP assignment and DNS resolution must be handled separately.
Monitoring: Prometheus and Grafana can be installed for monitoring, but this adds another layer of complexity and resource consumption that is overkill for a single server.
Updates: Each component updates independently. Security patches may be missed. Version conflicts between components can break the entire setup.
## The aiOS Solution
## aiOS replaces all of this complexity with a streamlined experience
1.	Download the aiOS ISO file (target size under 1GB)
2.	Flash it to a USB drive
3.	Boot the target machine from USB
4.	Answer three simple setup questions (disk, password, network)
5.	Open a browser and navigate to the machine's address
6.	Click "Install Model" to download your first AI model
7.	Your entire network now has access to a private AI server

---

## Why aiOS Exists
Current operating systems are designed for general-purpose computing. They must satisfy the needs of desktop users, developers, server administrators, and enterprise deployments simultaneously. This means they include hundreds of services and packages that have nothing to do with AI inference.
When you install Ubuntu Server to run AI models, here is what you get alongside your inference engine: printing services (CUPS), audio stacks (PulseAudio or PipeWire), Bluetooth daemons, desktop environment components, snap package manager with its daemon, cloud-init for cloud deployments, multipath storage tools, RAID management utilities, LVM volume management, games, office suites, media players, compilers, development headers, and locale files for over 200 languages.
None of these serve AI inference. They consume disk space, RAM, CPU cycles, and boot time. They increase the attack surface for security vulnerabilities. They complicate updates and system maintenance.
aiOS takes the opposite approach. Every component included in the operating system exists to serve one purpose: running AI inference on your network.
## What aiOS Removes
## The following components are intentionally excluded from aiOS
•	Desktop environments and window managers (save 2GB+ of RAM for model inference)
•	Printing services (CUPS, avahi-daemon)
•	Audio stacks (PulseAudio, PipeWire, ALSA utilities)
•	Bluetooth daemons and firmware
•	WiFi firmware for uncommon chipsets (optional install available)
•	Snap package manager and its daemon
•	Flatpak package manager
•	Cloud-init (not deploying to cloud providers)
•	Multipath storage tools, MDADM RAID, LVM volume management
•	Games, office suites, media players, image viewers
•	Compilers, build tools, development headers
•	Manual pages and documentation for removed packages
•	Locale files beyond en_US (saves hundreds of megabytes)
## What aiOS Keeps
## Only essential components remain
•	Linux kernel optimized for the target hardware
•	systemd for service management and supervision
•	Network stack with basic configuration tools
•	SSH server for emergency administrative access
•	Container runtime for inference engine isolation
•	GPU drivers (NVIDIA CUDA, AMD ROCm) auto-detected and installed
•	aiOS core management daemon
•	Web dashboard for system management
The result is an operating system where the base installation is under 1GB and idle RAM consumption is under 500MB (excluding loaded AI models). Every available system resource can be dedicated to inference workloads.

---

## Core Principles
AI First: Every architectural decision, every package inclusion, every configuration default prioritizes AI inference workloads above all other considerations.
Lightweight: The base operating system installs in under 1GB. Idle RAM usage stays under 500MB. Only essential services run. Nothing is included that does not directly support inference.
Privacy by Default: Everything runs locally on your hardware. No telemetry is collected. No data is sent to cloud services. No accounts are required. No subscriptions exist. Your prompts, your responses, your data remain entirely within your network.
Appliance Model: aiOS is designed to be installed and forgotten. It operates as an appliance, not a general-purpose computer. Users should not need to SSH into the machine for routine operations. Everything is manageable through the web dashboard.
Network Native: The operating system is built from the ground up to serve your entire network. The dashboard is accessible from any browser. The API is available to any application. Models are shared resources for all authorized users on the network.
Self-Updating: The operating system, inference engines, and models update automatically without user intervention. Security patches are applied promptly. Updates are atomic with automatic rollback on failure.
Modular: Inference engines run in isolated containers. Engines can be added, removed, or updated independently. The platform is extensible through a documented plugin API. Users are not locked into any single inference backend.
Single Binary Core: The core management daemon is a single statically-compiled binary. It requires no runtime dependencies, no language interpreters, and no external services to function. This simplifies deployment, reduces failure modes, and eases debugging.
API Driven: All system functionality is exposed through versioned REST APIs. The web dashboard is a consumer of these APIs, not a privileged component. CLI tools, third-party integrations, and custom scripts all use the same documented interfaces.
Open Source: The project is licensed under MIT. All development happens in public. Architecture decisions are documented and open for community input. The roadmap is public. Governance is community-driven.

---

## Who is aiOS For?
## Homelab Enthusiasts
You already run services like Plex for media streaming, Home Assistant for home automation, and TrueNAS for network storage. Your server rack is a source of pride. Now you want to add a private AI server to your setup.
aiOS runs on bare metal or as a virtual machine on your existing hypervisor. One installation provides AI access to every device in your home. Your phone, laptop, desktop, and smart home devices can all query your private AI without sending data to cloud services. Family members get their own API keys with usage limits.
## Small Development Teams
Your startup purchased an RTX 4090 for the office. Five developers need AI access for different tasks. Alice is testing prompts. Bob is generating embeddings for RAG applications. Carol is experimenting with code generation models. Dave needs vision model access. Eve wants to run evaluations.
Without aiOS, you would need Kubernetes, GPU device plugins, monitoring stacks, and significant DevOps time. With aiOS, you install once, create API keys for each developer, set rate limits, and everyone gets fair access to the shared GPU resource. No Kubernetes required.
## Privacy-Conscious Professionals
You work with sensitive data. Client legal documents. Patient medical records. Proprietary source code. Trade secrets. Financial projections. You cannot send this data to OpenAI, Anthropic, or Google. The compliance implications are unacceptable.
aiOS gives you ChatGPT-quality AI that never leaves your building. All inference happens on your hardware. No data is transmitted externally. No third party has access to your prompts or responses. You maintain complete data sovereignty while still benefiting from modern AI capabilities.
## Small Businesses
Law firms need document summarization. Accounting practices need data extraction. Medical offices need transcription. Architecture studios need design assistance. These organizations want AI capabilities but cannot risk sending client data to cloud providers.
aiOS provides a turnkey AI appliance for office networks. Non-technical staff access AI through a familiar chat interface. IT staff manage everything through a simple dashboard. No cloud subscriptions. No data leakage risk. No complex infrastructure.
## Edge Deployments
Factory floors need real-time quality inspection. Retail stores need inventory analysis. Research stations need offline data processing. Rural clinics need diagnostic assistance. These locations often have limited or unreliable internet connectivity. AI must work offline.
aiOS runs on commodity hardware with no cloud dependency. Models download once during setup. All inference happens locally. The system operates indefinitely without internet access. Updates can be applied manually via USB when connectivity is available.

---

## What aiOS is NOT
## It is important to be clear about what aiOS does not aim to be
Not a desktop operating system. aiOS has no graphical desktop environment. There is no window manager. There is no display output beyond the initial setup screen. It is a headless server operating system managed through a web browser.
Not a general-purpose Linux distribution. You cannot install arbitrary packages. You cannot run apt install to add desktop software. aiOS is a single-purpose appliance, not a flexible platform. This constraint enables the lightweight and reliable characteristics of the system.
Not a cloud service. aiOS runs entirely on your hardware. There is no cloud component. No accounts are created with any service. No data is synchronized to external servers. The project does not operate any infrastructure.
Not an AI model trainer. aiOS is optimized for inference only. Training, fine-tuning, and model development are not supported. Use dedicated training frameworks and platforms for those workflows.
Not a replacement for your daily driver. Continue using macOS, Windows, or Ubuntu for your personal computing. aiOS runs on dedicated hardware as a network appliance that you access from your primary devices.
Not yet another inference engine. aiOS does not implement its own model inference. It is the platform that manages existing inference engines like Ollama, vLLM, and ComfyUI. The value is in the orchestration, management, and user experience, not in reimplementing token generation.
Not an Ollama competitor. Ollama is a supported inference backend that runs on aiOS. The project aims to make Ollama easier to deploy, manage, and share across a network, not to replace it.
Not a Kubernetes distribution. aiOS does not use Kubernetes. It does not require knowledge of pods, deployments, services, or ingress. Simple container isolation handles the dependency management between inference engines.

---

## Features
## Installation Methods
## aiOS offers two installation paths
## Installer Script (Available Now for Early Testing)
For users with an existing Ubuntu Server 24.04 LTS installation, a single command transforms the system into aiOS. The script handles hardware detection, GPU driver installation, package stripping, and service deployment automatically.
## ISO Image (Coming in Phase 3)
A downloadable ISO file under 1GB in size. Users flash it to a USB drive using balenaEtcher or the dd command. The machine boots from USB and presents a three-screen installer asking only for target disk, admin password, and network configuration. After installation completes and the system reboots, the machine is a fully functional AI appliance.
## Web Dashboard
The dashboard is the primary interface for managing aiOS. It is accessible from any browser on the local network.
System Overview: Displays CPU usage, RAM consumption, disk space utilization, and system uptime in a clean, at-a-glance format.
GPU Monitor: Shows real-time VRAM usage, GPU temperature, utilization percentage, power draw in watts, and any active throttling status. Historical graphs allow trending analysis over time.
Model Library: A browsable catalog of available AI models. Each model shows its name, description, available quantization sizes, disk space required, and a one-click install button. Installed models can be deleted, updated, or configured from this interface.
API Management: Create and revoke API keys. Set rate limits per key. Restrict key access to specific models. View usage statistics per key including request counts, token generation totals, and average latency.
Network Settings: Configure hostname, switch between DHCP and static IP, set DNS servers, and integrate with Tailscale or WireGuard for secure remote access.
User Management: Create admin accounts, family user accounts with limited permissions, and API-only service accounts for application integration.
Update Center: View available updates for the base operating system, inference engines, and models. Read changelogs before applying updates. Configure automatic update policies.
Logs: Searchable, filterable log viewer showing system events, inference requests, errors, and security audit entries.
## One-Click Model Installation
The model library allows users to browse and install AI models with a single click. No command line interaction is required.
## General Purpose Language Models
The system supports Llama 3 in 8B and 70B parameter sizes for general chat and reasoning tasks. Qwen 2.5 is available in 7B, 14B, 32B, and 72B sizes for multilingual applications and long context windows. DeepSeek V3 comes in 7B and 67B sizes optimized for code, mathematics, and logical reasoning. Mistral provides efficient 7B and 8x7B mixture-of-experts architectures. Gemma 2 offers Google ecosystem compatibility in 9B and 27B sizes.
## Specialized Models
Code generation is supported through CodeLlama, Qwen Coder, DeepSeek Coder, and StarCoder models. Vision understanding uses Llama Vision, Qwen VL, LLaVA, and CogVLM. Speech processing includes Whisper for speech-to-text conversion and Piper for text-to-speech synthesis. Image generation is available through Stable Diffusion, FLUX, and SDXL models. Embedding models including BGE, Nomic, and Jina support retrieval-augmented generation and semantic search applications.
## Model Management Features
All downloaded models undergo automatic checksum verification to ensure file integrity. Interrupted downloads resume from where they stopped without restarting. Users can select quantization levels when installing models, with Q4_K_M as the balanced default and Q5, Q8, and F16 available for quality-sensitive applications. Storage usage is monitored with warnings when disk space runs low. Background updates keep models current with automatic rollback capability if updated versions fail validation.
## Network-Wide Access
Once aiOS is running, every device on the local network can access AI capabilities.
The web dashboard is available at the machine's hostname or IP address on the local network. The OpenAI-compatible API endpoint exposes the standard chat completions interface that works with hundreds of existing tools and libraries.
Compatible clients include VS Code with Continue, Cody, or Cline extensions for AI-assisted software development. Obsidian note-taking software with AI plugins for smart knowledge management. Home Assistant for AI-powered conversation agents in home automation. Open WebUI as an alternative web interface. LangChain and LlamaIndex for custom application development. Any programming language through simple HTTP requests. iOS Shortcuts for mobile AI access from iPhones and iPads.
## Privacy and Security
Security is designed into aiOS from the foundation, not bolted on afterward.
Local-Only Operation: All inference runs on the device. No prompts, responses, or usage data leave the local network. There is no telemetry collection. No usage statistics are reported to any external service.
API Authentication: All API endpoints require authentication. API keys are hashed using bcrypt before storage. Keys can be scoped to specific models and assigned rate limits.
Rate Limiting: Per-key rate limits prevent any single user or application from monopolizing GPU resources. Limits can be configured per key with different thresholds for different use cases.
Audit Logging: Every inference request is logged with timestamp, API key identifier, model name, input token count, output token count, and request latency. Logs are stored locally and never transmitted externally.
Network Binding: The dashboard and API bind to the local network interface by default. They are not exposed to the public internet unless explicitly configured.
HTTPS Encryption: Self-signed certificates are automatically generated for local network access. Let's Encrypt integration is available for users who choose to expose aiOS to the internet.
Firewall Configuration: A pre-configured firewall allows only the dashboard port and API port. All other ports are blocked by default.
SSH Hardening: SSH access requires key-based authentication. Password authentication is disabled. Rate limiting and fail2ban protect against brute force attempts.
Read-Only Root: In future releases, the root filesystem will be mounted read-only with only model storage and configuration directories remaining writable. This prevents unauthorized system modifications.
Atomic Updates: Future releases will use A/B partition updates. The system installs updates to an inactive partition and only switches over after successful health checks. Failed updates roll back automatically.
## Built-In Monitoring
aiOS includes comprehensive monitoring without requiring separate Prometheus or Grafana installations.
GPU Metrics: VRAM usage (absolute and percentage), GPU utilization percentage, temperature in Celsius, power draw in watts, and throttling status are displayed in real-time on the dashboard.
System Metrics: CPU utilization, RAM usage, disk space consumption, and network throughput are tracked continuously.
Inference Metrics: Requests per minute, tokens generated per second, average and P99 latency, current queue depth, and active model count are calculated and displayed.
External Integration: A Prometheus-compatible metrics endpoint is available at the standard path for users who wish to integrate aiOS with existing monitoring infrastructure.
## Automatic Updates
The update system keeps aiOS current without requiring manual intervention.
Base OS Updates: Security patches are applied automatically. Major version upgrades require explicit user confirmation through the dashboard.
Inference Engine Updates: New container images are pulled automatically when available. Health checks run after each update. Failed health checks trigger automatic rollback to the previous working version.
Model Updates: Users are notified when updated model versions are available. Updates can be configured to apply automatically or wait for manual approval.
aiOS Core Updates: The management daemon checks for new releases and can self-update atomically. The old binary is preserved for rollback if the new version fails to start.
## Plugin Architecture
aiOS can be extended through a documented plugin system.
Inference Backend Plugins: Community members can add support for new inference engines beyond the defaults. Potential additions include TensorRT-LLM for maximum NVIDIA performance, SGLang for structured generation, and custom engines for specialized hardware.
Authentication Provider Plugins: Beyond the built-in API key system, plugins can add LDAP integration for enterprise directories, OpenID Connect for single sign-on, and Tailscale identity for zero-configuration secure access.
Storage Backend Plugins: Model storage can be extended to network filesystems (NFS), object storage (S3-compatible), or clustered storage for multi-node deployments.
Notification Plugins: System alerts and status updates can be delivered through email, Discord webhooks, Slack integration, or generic webhook endpoints.
Plugins run in isolated containers with defined resource limits. The plugin API is versioned and documented. A community plugin registry will enable discovery and installation through the dashboard.

---

## Architecture
## High-Level Design
The aiOS architecture is organized in layers, each with clear responsibilities and interfaces.
Network Clients Layer: Browsers accessing the dashboard, code editors using the API, mobile apps, smart home systems, and custom scripts all communicate with aiOS through standard HTTPS and REST protocols.
aiOS Core Service Layer: This is the central management component. It contains the web server serving the dashboard, the API gateway exposing the OpenAI-compatible endpoint, and the administration API for system management. Behind these interfaces, the management layer handles authentication, model lifecycle, updates, and monitoring. The orchestration layer manages request scheduling, queuing for concurrent users, and container lifecycle operations.
Container Runtime Layer: Docker provides isolated environments for each inference engine. Ollama handles general-purpose language model serving. vLLM provides high-throughput production serving for demanding workloads. ComfyUI manages image generation workflows. Custom community plugins run in their own containers. The NVIDIA Container Toolkit ensures efficient GPU passthrough to each container.
GPU Driver Layer: Auto-detected and auto-installed drivers for NVIDIA CUDA and AMD ROCm provide the hardware interface. Future support for Intel oneAPI is planned.
Base Operating System Layer: A minimal Linux installation provides only the kernel, systemd for service management, network stack, SSH server, and container runtime. Nothing else is included.
## Component Details
aiOS Core Daemon: A single statically-compiled binary written in Go. It requires no runtime dependencies. The daemon serves the web dashboard, exposes the API endpoints, manages authentication and authorization, orchestrates model downloads and lifecycle, monitors GPU and system health, schedules inference requests across available engines, and manages container lifecycles for inference backends. The daemon uses SQLite for persistent state storage with an in-memory ring buffer for high-frequency telemetry data.
Inference Engines: Each engine runs in an isolated Docker container. This provides dependency isolation so each engine can have its own Python version, CUDA libraries, and dependencies without conflicts. It enables independent updates so updating vLLM does not affect an Ollama installation. It provides security isolation so a vulnerability in one engine does not compromise others. It simplifies the plugin model since community engines can be packaged as standard container images.
Container Runtime: Docker with the NVIDIA Container Toolkit provides the isolation layer. Containers were chosen over native processes because inference engines have complex, often conflicting dependency requirements. Container isolation solves this problem without requiring aiOS to maintain compatibility matrices between engine versions.
Base Operating System: In early releases, a heavily stripped Debian installation provides the foundation. Using debootstrap with the minbase variant and aggressive package exclusion, the installed size is approximately 800MB including GPU drivers. In future releases, a Buildroot-based custom image will reduce this to approximately 300MB with a custom kernel, read-only root filesystem, and atomic A/B partition updates.

---

## Technology Stack
The following technologies have been selected for aiOS based on the principles of simplicity, reliability, and minimal resource consumption.
Core Daemon Language: Go has been chosen for the central management daemon. It compiles to a single static binary with no runtime dependencies. Its concurrency model maps well to the request handling and scheduling requirements. Compilation is fast, enabling rapid development iteration. The resulting binary is small and efficient.
Web Dashboard: React with TypeScript and Tailwind CSS provides a modern, maintainable frontend. TypeScript catches errors at compile time. React's component model enables code reuse across the dashboard. Tailwind CSS keeps the stylesheet small and consistent.
Database: SQLite stores all persistent state. It requires zero administration. There are no connection pools to configure, no authentication to manage, and no separate process to monitor. The entire database is a single file that can be backed up by copying. SQLite is the most tested database engine in the world and is perfectly sufficient for the configuration and metadata storage needs of aiOS.
Caching: Telemetry data is stored in an in-memory ring buffer within the Go daemon process. This provides sub-microsecond access times for the dashboard without requiring an external cache service like Redis.
Container Runtime: Docker with the NVIDIA Container Toolkit is the industry standard for GPU container workloads. It is well-documented, widely understood, and supported by all major inference engines.
Base Operating System: Debian netinst serves as the initial base for its excellent NVIDIA driver compatibility and glibc support. Buildroot is planned as the future base for true minimalism with custom kernel configurations and sub-300MB images.
GPU Support: NVIDIA CUDA 12.x is the primary target given its dominance in AI workloads. AMD ROCm 6.x support is implemented in parallel. Intel oneAPI support is planned for future releases as Intel Arc GPUs gain AI relevance.
API Protocols: REST with OpenAI-compatible endpoints ensures compatibility with the massive ecosystem of tools built for the OpenAI API format. gRPC is planned for high-throughput streaming scenarios where its binary protocol provides efficiency advantages.
Authentication: bcrypt-hashed API keys provide the default authentication mechanism. The system is extensible to support OIDC and LDAP through the plugin architecture for enterprise deployments.
Monitoring: Built-in metrics collection feeds the dashboard. A Prometheus-compatible endpoint enables integration with external monitoring stacks for users who have existing observability infrastructure.

---

## Development Roadmap
Phase 0: Research and Validation (Current)
The project is currently in the planning and validation phase. Architecture documents are published for community feedback. The technology stack is being finalized. A prototype core daemon demonstrating GPU detection capabilities is under development. An alpha version of the installer script is being tested. Community feedback is being gathered through GitHub Discussions and Discord.
Phase 1: Minimum Viable Product (Target: Q3 2026)
This phase delivers the core installer and basic functionality.
The installer script will be stable and capable of transforming a fresh Ubuntu Server 24.04 installation into a functional aiOS system. It will auto-detect NVIDIA and AMD GPUs and install appropriate drivers. It will deploy Ollama in a Docker container with GPU access. It will strip over 100 unnecessary packages from the base system. It will configure the firewall and enable automatic updates.
The core daemon will provide health check endpoints, GPU monitoring, basic model management through Ollama's API, and SQLite-backed configuration storage.
The web dashboard will display system status, GPU metrics, installed models, and a simple chat interface for interacting with loaded models.
A CLI tool will support basic commands including system status queries, model listing, and model installation.
Phase 2: Multi-User and Production Features (Target: Q4 2026)
This phase adds the features needed for team and production use.
API authentication will include key generation, management, rate limiting, and per-key model access controls. Request queuing will handle concurrent users with priority queues and queue depth monitoring visible in the dashboard. Multiple models will be loadable simultaneously with VRAM budget management and preloading capabilities.
The dashboard will expand to include user management, API key administration, usage statistics, and a log viewer.
Additional inference backends will be supported including vLLM for high-throughput serving and ComfyUI for image generation workflows.
Update management will move to the dashboard UI with changelog viewing and approval workflows.
Phase 3: ISO Release (Target: Q1 2027)
This phase delivers the standalone operating system image.
A custom Debian-based ISO will be created with a target size under 1GB. It will include a simple graphical or text-based installer with only three configuration screens. Hardware detection will be fully automatic. The system will be pre-configured for headless operation.
Production hardening will include automatic HTTPS certificate generation, SSH hardening, comprehensive audit logging, and backup and restore functionality.
The plugin system version 1 will launch with a stable API, a community plugin registry, and plugin management through the dashboard.
Official documentation will be published including architecture guides, deployment tutorials, API references, and video walkthroughs.
Phase 4: True Minimalism (Target: Q3 2027)
This phase achieves the ultimate lightweight vision.
The Buildroot-based OS image will reduce the ISO size to under 300MB. The root filesystem will be read-only with only model storage and configuration remaining writable. A/B partition updates will enable atomic upgrades with automatic rollback on failure. Boot time will be under five seconds from power-on to inference-ready.
Advanced features will include optional multi-node clustering, distributed inference across multiple machines, high availability configurations, and enterprise single sign-on integration.
## Future Vision (Post Phase 4)
Long-term goals include hardware appliance partnerships with manufacturers, an optimized build for Raspberry Pi and NVIDIA Jetson platforms, a mobile management application, a model marketplace with community ratings and reviews, a basic fine-tuning interface supporting LoRA adapters, a visual RAG pipeline builder, and agent framework integration for autonomous AI workflows.

---

## Project Structure
## The aiOS repository is organized into the following directories
installer directory: Contains the installer script that transforms Ubuntu Server into aiOS. Includes GPU detection scripts, driver installation automation, and package removal logic. The ISO subdirectory contains configuration for building the standalone installer image. The preseed subdirectory contains Debian preseed configuration files for automated installation.
daemon directory: Contains the aiOS core daemon written in Go. The cmd subdirectory holds the main entry point. The api subdirectory contains REST and gRPC handlers organized by function (dashboard, OpenAI-compatible endpoint, admin management). The auth subdirectory handles authentication and authorization. The models subdirectory manages model lifecycle. The scheduler subdirectory implements request scheduling and queuing. The gpu subdirectory handles GPU monitoring. The containers subdirectory manages Docker container lifecycle. The updates subdirectory handles update orchestration. The storage subdirectory contains the SQLite interface. The metrics subdirectory exposes Prometheus-compatible metrics. The config subdirectory manages system configuration.
cli directory: Contains the aiOS command-line tool written in Go. The cmd subdirectory defines CLI commands. The client subdirectory provides an API client library for communicating with the daemon.
dashboard directory: Contains the web dashboard built with React and TypeScript. The src directory contains components, pages, custom hooks, API client code, and state management stores. The public directory holds static assets.
plugins directory: Contains specifications for the plugin system, example plugin implementations, and plugin API documentation.
docs directory: Contains comprehensive documentation including architecture descriptions, development guides, deployment instructions, API reference material, and frequently asked questions.
scripts directory: Contains build scripts, test automation, and release tooling.
tests directory: Contains integration tests and end-to-end tests.
benchmarks directory: Contains performance benchmarking tools and results.
.github directory: Contains GitHub Actions workflow definitions for continuous integration and deployment.

---

## Contributing
aiOS is in its early stages and welcomes contributions of all kinds from developers, designers, writers, and testers.
## How to Contribute
First, read the CONTRIBUTING.md file for detailed guidelines and the CODE_OF_CONDUCT.md file for community standards.
Find something to work on by checking open issues on GitHub, looking for issues tagged as good first issue, or proposing new features in the GitHub Discussions area.
Set up a development environment by cloning the repository and running the development setup script. Make your changes following the project's coding standards and including tests where appropriate. Submit a pull request describing your changes and referencing any related issues.
## Contribution Areas
Core Daemon development requires Go programming skills, systems programming experience, and API design knowledge. This is critical infrastructure work with high impact on the project.
GPU Integration requires experience with CUDA, ROCm, and GPU driver architecture. This is critical for supporting diverse hardware configurations.
Web Dashboard development requires React, TypeScript, and UI/UX design skills. This is high-impact work that directly affects user experience.
Installer development requires Bash scripting, Linux packaging knowledge, and Debian system administration experience. This is high-impact work that determines the first user experience.
ISO Build engineering requires experience with Linux from scratch, Buildroot, or Yocto. This is specialized work for achieving true OS minimalism.
Documentation writing requires technical writing ability and the patience to create clear tutorials and reference material. This is high-impact work that helps users succeed.
Testing requires experience with Go testing frameworks, end-to-end testing tools, and CI/CD pipeline configuration.
Security engineering requires Linux hardening expertise and authentication system design knowledge.
Benchmarking requires performance analysis skills and profiling experience.
Plugin development requires diverse skills depending on the plugin type. Example plugins help grow the ecosystem.
Translation makes aiOS accessible to non-English speaking users.
Community support on GitHub, Discord, and forums helps users succeed and provides valuable feedback to developers.
## Development Philosophy
## Contributors should follow these principles
Keep implementations simple. Prefer simplicity over cleverness. The next person reading your code should understand it quickly.
The core daemon is a single static binary. Avoid introducing new services or external dependencies. Justify any addition thoroughly.
Document as you build. Architecture decisions should be captured in Architecture Decision Records. API changes must include documentation updates.
Test before optimizing. Make it correct first, then make it fast. Premature optimization creates complexity without proven benefit.
Security is never optional. Every endpoint requires authentication. Every input must be validated. Assume all inputs are malicious until proven otherwise.
Respect the user. No telemetry without explicit opt-in. No dark patterns. No vendor lock-in. Users should always be able to export their data and migrate away.

---

## Community
## Communication Channels
GitHub Discussions serves as the primary venue for ideas, RFCs, and questions. This is where major feature proposals are discussed and refined before implementation begins.
Discord provides real-time chat for community support, development coordination, and casual discussion. This is the best place for quick questions and getting to know other contributors.
GitHub Issues tracks bug reports and feature development. Check existing issues before creating new ones to avoid duplicates.
Reddit hosts community showcases, deployment stories, and broader discussions about the project's direction.
## Community Guidelines
## All community spaces operate under the following expectations
Be respectful and constructive in all interactions. Assume good intent from others. Disagreement is natural but must remain professional.
Help others learn. Everyone was a beginner once. Patient explanations strengthen the community.
Celebrate contributions of all sizes. A documentation fix is as valuable as a major feature. Every improvement moves the project forward.
Avoid AI-generated spam in discussions. Thoughtful human contributions are valued over volume.
English is the primary language for development discussions. Translations of documentation and interfaces are welcome contributions.
## Decision Making
## aiOS uses a Request for Comments process for major changes
A proposal begins as a GitHub Discussion where the community provides initial feedback. If the idea gains support, it becomes a formal RFC with a detailed design document. The community reviews the RFC and provides structured feedback. The core team reviews all feedback and makes a decision. Approved RFCs move to implementation with community involvement.
All RFCs are public. All decisions are documented with their rationale. This ensures the project's direction is transparent and the community's voice is heard.

---

## Frequently Asked Questions
## General Questions
## Is aiOS ready for production use?
No. aiOS is currently in pre-alpha status. It is not suitable for production workloads. Follow the roadmap for timeline estimates on stable releases.
## Can aiOS run on a Raspberry Pi?
CPU-only inference works on Raspberry Pi 5 with 8GB of RAM for small models. GPU inference requires an NVIDIA or AMD discrete GPU. A Pi-optimized build is planned for Phase 4.
## Does aiOS support AMD GPUs?
Yes, AMD GPUs are supported through the ROCm stack. Support is planned for the Phase 1 installer alongside NVIDIA support.
## Does aiOS support Intel Arc GPUs?
Support is planned through Intel oneAPI but is not included in the initial releases. Intel GPU support will be added based on community demand and hardware availability.
## Can I install aiOS alongside my existing operating system?
aiOS is designed for dedicated hardware. Dual-boot configurations are not supported. If you need to run aiOS alongside other operating systems, run it as a virtual machine on your hypervisor.
## Does aiOS require internet access?
Internet access is needed for initial model downloads and system updates. After models are downloaded, inference works fully offline. For completely air-gapped deployments, models can be transferred manually via USB drive.
## Technical Questions
## What is included in the base operating system?
The base OS includes only: Linux kernel, systemd for service management, network stack for connectivity, SSH server for administrative access, Docker for container isolation, GPU drivers for hardware acceleration, and the aiOS daemon for management. Nothing else is included. There is no desktop environment, no printing system, no audio stack, and no unnecessary services.
## Why does aiOS use Docker? Is that not heavy for a lightweight OS?
Docker provides dependency isolation between inference engines without requiring aiOS to maintain compatibility between them. The overhead is approximately 50MB of RAM for the Docker daemon, which is minimal compared to the complexity Docker eliminates. Without containers, aiOS would need to solve the same dependency isolation problems that containers already solve. The trade-off favors using proven technology.
## Can I SSH into an aiOS machine?
Yes, SSH access is enabled for administrative purposes. Key-based authentication is required by default. Password authentication is disabled for security. SSH is intended for emergency troubleshooting, not routine management, which should be done through the dashboard.
## What happens if an update breaks the system?
The update system creates a checkpoint before applying changes. After an update, health checks verify that services are running correctly. If health checks fail, the system automatically rolls back to the previous working state. This applies to OS updates, inference engine updates, and aiOS daemon updates.
## How do I backup my aiOS installation?
Model files and system configuration are stored in a single directory. Backing up this directory captures all important state. A fresh installation plus restoring this backup directory results in a fully recovered system. Detailed backup instructions will be provided in the documentation.
## Can aiOS be exposed to the public internet?
Yes, with appropriate security precautions. HTTPS encryption is required for internet exposure. Built-in Tailscale integration is the recommended method for secure remote access, as it provides authentication and encryption without exposing ports to the public internet. Direct internet exposure with port forwarding is possible but requires careful firewall configuration.
## Model Questions
## How are models stored on disk?
Models are stored in the aiOS data directory in GGUF format by default. Each model includes its weight file, tokenizer configuration, and metadata. The storage location is configurable for users who want to use a dedicated storage drive.
## Can I use my own custom models?
Yes, custom models can be added by placing GGUF format files in the models directory. Custom model sources can also be configured to pull from private repositories or alternative download locations.
## How does model quantization work?
aiOS defaults to Q4_K_M quantization when downloading models, which provides a good balance between quality and file size. Users can select Q5_K_M for higher quality, Q8_0 for near-lossless quality, or F16 for full precision when storage and VRAM permit. The choice is presented during model installation.
## Can multiple users access different models simultaneously?
Yes, if VRAM capacity permits. aiOS manages VRAM allocation across loaded models. The scheduler tracks which models are in memory and routes requests accordingly. When VRAM is exhausted, Phase 2 will include intelligent model swapping to load requested models and unload idle ones automatically.

---

## Comparisons
## aiOS Compared to Manual Setup
Manual Setup on Ubuntu Server: The user must download a 6GB ISO, install the operating system, configure SSH, research GPU driver installation procedures, fight with secure boot and nouveau conflicts, install Docker and the NVIDIA Container Toolkit separately, pull inference engine images, create systemd service files manually, configure firewall rules, set up a reverse proxy for web access, and maintain each component individually. Total time for an experienced Linux user: 2-4 hours. For a novice: potentially days.
aiOS Installation: The user downloads a sub-1GB ISO, flashes it to USB, boots the machine, answers three setup questions, and opens a browser. The dashboard is immediately available. Models install with one click. The system updates itself automatically. Total time: 15-30 minutes regardless of Linux experience.
## aiOS Compared to Ollama
Ollama is an excellent inference engine that aiOS uses internally. Ollama provides one-command model serving for a single user. aiOS builds on Ollama's capabilities by adding multi-user support with API keys and rate limiting, a web dashboard for management, automatic GPU driver installation, an operating system optimized for inference, automatic updates for all components, and network-wide access configuration out of the box.
aiOS is not an Ollama competitor. It is a platform that makes Ollama easier to deploy and share. Users who are happy running Ollama on their desktop for personal use do not need aiOS. Users who want to deploy Ollama as a shared network service for a team or family will find aiOS provides the missing management layer.

---

## License
This project is licensed under the MIT License. See the LICENSE file for complete terms.
The MIT License permits commercial use, modification, distribution, and private use. It requires only that the license notice and copyright notice are included in copies or substantial portions of the software. The software is provided as-is without warranty.

---

## Status
This project is currently in the pre-alpha planning phase. The architecture is under active discussion. The roadmap is open for community input. Contributors are welcome to help shape the direction and implementation.

---

## Contact and Links
GitHub Repository: github.com/aios/aios
Discord Community: discord.gg/aios
GitHub Discussions: github.com/aios/aios/discussions
Reddit Community: reddit.com/r/aios
