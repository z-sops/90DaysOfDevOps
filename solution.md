# Docker Terminologies and Components

## Key Docker Terminologies

### 1. **Image**
A Docker image is a lightweight, standalone, and executable package that contains everything needed to run an application, including:
- Application code
- Runtime environment
- System libraries
- Dependencies
- Configuration files

Images are built from a Dockerfile and serve as templates for creating containers. They are immutable and can be stored in registries.

### 2. **Container**
A container is a running instance of a Docker image. Key characteristics:
- Isolated process that runs on the host operating system
- Shares the host OS kernel but has its own filesystem, networking, and process space
- Lightweight and fast to start/stop
- Can be created, started, stopped, moved, and deleted
- Multiple containers can run from the same image

### 3. **Dockerfile**
A text file containing a series of instructions used to build a Docker image. It includes:
- Base image specification (FROM)
- Commands to install dependencies (RUN)
- File copying instructions (COPY/ADD)
- Environment variables (ENV)
- Port exposure (EXPOSE)
- Default execution command (CMD/ENTRYPOINT)

### 4. **Volume**
A mechanism for persisting and sharing data between containers and the host system:
- **Named Volumes**: Managed by Docker, stored in Docker's storage area
- **Bind Mounts**: Direct mapping between host directory and container directory
- **tmpfs Mounts**: Stored in host memory, temporary storage
- Volumes persist even when containers are removed

### 5. **Network**
Docker networking enables communication between containers and external systems:
- **Bridge Network**: Default network for containers on same host
- **Host Network**: Container shares host's network stack
- **Overlay Network**: Enables communication across multiple Docker hosts
- **None Network**: Disables networking for a container

### 6. **Registry**
A service for storing and distributing Docker images:
- **Docker Hub**: Default public registry
- **Private Registries**: Self-hosted or cloud-based private image storage
- **Repository**: Collection of related images with different tags

### 7. **Tag**
A label applied to Docker images to identify different versions:
- Format: `repository:tag` (e.g., `nginx:latest`, `node:18-alpine`)
- If no tag specified, `latest` is used by default
- Helps in version management and deployment strategies

## Main Docker Components

### 1. **Docker Engine**
The core runtime that manages Docker containers and images:

#### **Docker Daemon (dockerd)**
- Background service running on host system
- Manages Docker objects (images, containers, networks, volumes)
- Listens for Docker API requests
- Handles container lifecycle operations

#### **Docker Client (docker)**
- Command-line interface for interacting with Docker
- Sends commands to Docker daemon via REST API
- Can communicate with remote Docker daemons

#### **Docker API**
- REST API used by clients to communicate with Docker daemon
- Enables programmatic control of Docker operations
- Used by Docker CLI, Docker Compose, and third-party tools

### 2. **Docker Hub**
Docker's official cloud-based registry service:
- **Public Repository**: Free hosting for public images
- **Private Repository**: Secure hosting for proprietary images
- **Official Images**: Curated images maintained by Docker
- **Automated Builds**: Automatically builds images from source code repositories
- **Webhooks**: Triggers actions when images are pushed/pulled

### 3. **Docker Compose**
Tool for defining and running multi-container Docker applications:
- Uses YAML files (`docker-compose.yml`) to configure services
- Manages application stacks with single commands
- Handles service dependencies and networking
- Useful for development and testing environments

### 4. **Docker Desktop**
Integrated development environment for containerized applications:
- Available for Windows, macOS, and Linux
- Includes Docker Engine, Docker CLI, Docker Compose
- Provides GUI for container management
- Includes Kubernetes integration

## Component Interactions

### Image Creation Flow
1. **Developer** writes Dockerfile
2. **Docker Client** sends build command to Docker Daemon
3. **Docker Daemon** reads Dockerfile and creates image layers
4. **Completed Image** stored in local image cache

### Container Runtime Flow
1. **Docker Client** requests container creation from image
2. **Docker Daemon** pulls image (if not locally available)
3. **Container** created with isolated filesystem, network, and processes
4. **Application** runs inside container environment

### Registry Interaction
1. **Docker Client** pushes/pulls images to/from registry
2. **Docker Hub/Registry** stores and serves images
3. **Authentication** handled for private repositories
4. **Image Layers** shared between similar images for efficiency

### Networking Communication
1. **Docker Daemon** creates virtual networks
2. **Containers** connect to networks for communication
3. **Port Mapping** enables external access to containerized services
4. **DNS Resolution** allows containers to find each other by name

## Benefits of Component Architecture

- **Separation of Concerns**: Each component has specific responsibilities
- **Scalability**: Components can be distributed across multiple hosts
- **Flexibility**: Different clients can interact with same Docker daemon
- **Security**: API-based communication enables secure remote operations
- **Ecosystem Integration**: Standard interfaces allow third-party tool integration
