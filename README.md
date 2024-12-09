# ⛵ Personal Kubernetes Cluster as Code

This repository contains the full Infrastructure-as-Code (IaC) setup for my personal Kubernetes cluster. It is designed for running and managing a production-grade Kubernetes environment with GitOps practices.

## 📂 Repository Structure

The repository is organized as follows:

.
├── .devcontainer/         # Development container configuration
├── .github/               # GitHub workflows for CI/CD
├── .taskfiles/            # Taskfile automation scripts
├── .vscode/               # VSCode workspace settings
├── bootstrap/             # Scripts and templates for provisioning
├── kubernetes/
│   ├── apps/              # Application manifests and HelmReleases
│   ├── bootstrap/         # Initial Flux and Talos deployment
│   └── flux/              # GitOps Flux configuration and repositories
└── scripts/               # Utility scripts

## ✨ Features

- **GitOps with Flux**: Automated deployment and management of cluster resources via Flux.
- **Scalability**: Designed for both small home-lab clusters and large-scale production setups.
- **Customizable App Deployments**: Applications are primarily managed using the [bjw-s AppTemplate](https://bjw-s.github.io/helm-charts), allowing tailored configurations for specific needs.
- **Secrets Management**: Integration with `sops` for secure secret management.
- **CNI and Networking**: Uses [Cilium](https://cilium.io/) for advanced networking and security.
- **Ingress Management**: Includes ingress-nginx for internal and external access to applications.
- **Monitoring and Observability**: Pre-configured monitoring stack (Prometheus, Grafana).
- **Storage**:
  - [Longhorn](https://longhorn.io): Distributed block storage for Kubernetes.
  - [MinIO](https://min.io): S3-compatible object storage.
  - [NFS Subdir External Provisioner](https://github.com/kubernetes-sigs/nfs-subdir-external-provisioner): Lightweight NFS-based storage provisioner.
  - [OpenEBS](https://openebs.io): Cloud-native storage for containers.

## 📦 Applications

The cluster hosts the following applications:

- **Immich**: Photo and video backup service with AI-based search capabilities.
- **Mastodon**: A decentralized social network instance.
- **Nextcloud**: A self-hosted productivity platform.
- **Paperless-ngx**: Document management system for organizing and digitizing your paperwork.

All these applications are deployed using the **[bjw-s AppTemplate](https://bjw-s.github.io/helm-charts)**, which provides a flexible and modular approach to application management. This ensures that each application is tailored to meet my personal requirements.

## 🔒 Security

- **Namespace `Security`**: A dedicated namespace for managing security-related services.
  - **Identity Provider**: Authentik is deployed to provide centralized authentication and SSO capabilities.
  - **Secrets Management**: external-secrets integrates with 1Password for secure, automated secrets management.
- **TLS Everywhere**: All applications are configured to use TLS, managed by `cert-manager` with Let's Encrypt, ensuring end-to-end encryption.
- **BSI Compliance**: TLS certificates are configured to meet the BSI's Technical Guideline TR-02102-2 standards.
- **ECDSA Certificates**: Preferred for stronger cryptography and improved performance.
- **Secrets Encryption**: Managed using `sops` to ensure secure storage and transmission of sensitive information.

## 🖧 Cluster Infrastructure

The Kubernetes cluster is hosted on a robust infrastructure provided by Netcup:

- **Nodes**: Three virtual root servers (RS 2000 G11) from Netcup, each equipped with:
  - **CPU**: 8 cores
  - **RAM**: 16 GB
  - **Storage**: 512 GB SSD
- **Firewall**: An OPNsense firewall is deployed on an additional virtual server at Netcup to:
  - Protect the cluster.
  - Facilitate connections to local home networks.
- **NFS Storage**: Another dedicated virtual server at Netcup provides NFS storage for the cluster.

For more details about Netcup, check their [website](https://www.netcup.com/de/?ref=97728).

[![Netcup](https://www.netcup.com/uploads/netcup_hlogo_2019_b110h50_32d03f6da4.png)](https://www.netcup.com/de/?ref=97728)

## 🌟 Acknowledgments

This cluster setup is inspired by and based on the exceptional [cluster-template](https://github.com/onedr0p/cluster-template) by **onedr0p**.

The template serves as a comprehensive foundation for GitOps-driven Kubernetes cluster management. It provides:
- **Best Practices**: Following modern standards in Kubernetes infrastructure.
- **Flexibility**: A highly modular and customizable design.
- **Community Support**: Extensive documentation and a supportive community.

Additionally, the cluster heavily relies on the excellent [Helm Charts](https://github.com/bjw-s/helm-charts) provided by **bjw-s**. The **AppTemplate** offered by bjw-s makes application management streamlined and highly customizable, allowing for tailored deployments that fit unique needs while maintaining consistency and reliability.

Special thanks to **onedr0p** and **bjw-s** for sharing these fantastic resources, which significantly enhanced the quality and efficiency of this cluster's setup!

📄 License

This repository is licensed under the MIT License.

🤝 Contributions

Contributions are welcome! Feel free to fork the repository and submit a pull request with your improvements or ideas.

For detailed information on each component or to raise an issue, visit the repository’s issues section.

Let me know if further adjustments are needed!
