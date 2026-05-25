# llama-cpp-dgx

A specialized build environment and containerization for `llama.cpp` optimized for NVIDIA DGX systems.

## Overview

This repository provides a `Dockerfile` and Kubernetes (Kaniko) build configurations for building `llama.cpp` with high-performance CUDA support. It is specifically tuned for modern NVIDIA architectures (Compute Capability 12.0 and 12.1).

## Features

- **CUDA Optimized:** Built using CUDA 12.9 on Ubuntu 24.04.
- **DGX Ready:** Default build architectures target H100 (`120`) and beyond (`121`).
- **Kubernetes Native:** Includes Kaniko job configurations for automated builds within a K8s cluster.
- **Multi-Stage Builds:** Produces a lean runtime image containing only the necessary binaries and libraries.
- **SOPS Protected:** Infrastructure secrets are managed using SOPS and `age`.

## Getting Started

### Prerequisites

- Docker or a Kubernetes cluster.
- [SOPS](https://github.com/getsops/sops) (for secret management).
- `age` (for SOPS encryption/decryption).

### Building Locally

```bash
docker build -t llama-cpp-dgx:latest --target server .
```

### Kubernetes Build

The `k8s/build/kaniko-job.yaml` can be used to trigger a build in your cluster:

```bash
kubectl apply -f k8s/build/kaniko-job.yaml
```

*Note: Ensure `ghcr-secret` is created (see `k8s/build/ghcr-secret.sops.yaml`).*

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
