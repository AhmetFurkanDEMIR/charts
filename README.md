# Demir Open Source Helm Charts

This repository contains open source Helm charts maintained by Ahmet Furkan Demir.

---

## Charts

### 1. Apache Ranger

A Helm chart for deploying [Apache Ranger](https://ranger.apache.org/) on Kubernetes.

- **Repository:** [AhmetFurkanDEMIR/charts](https://github.com/AhmetFurkanDEMIR/charts)
- **Chart Location:** `apache-ranger/`
- **Features:**
  - Deploys Apache Ranger with customizable configuration.
  - Supports PostgreSQL as a dependency.
  - Resource and service configuration.
- **Quick Install:**
  ```sh
  helm repo add apache-ranger https://ahmetfurkandemir.github.io/charts/demir-open-source/apache-ranger/

  helm upgrade --install apache-ranger apache-ranger/apache-ranger --version 0.1.0 -n apache-ranger --create-namespace
  ```
- **Documentation:** See [`apache-ranger/README.md`](demir-open-source/apache-ranger/README.md) for full usage and configuration.

---

### 2. Iceberg REST Fixture

A Helm chart for deploying the Iceberg REST Catalog Fixture with optional PostgreSQL and S3-compatible storage.

- **Repository:** [AhmetFurkanDEMIR/charts](https://github.com/AhmetFurkanDEMIR/charts)
- **Chart Location:** `iceberg-rest-fixture/`
- **Features:**
  - Deploys Iceberg REST Fixture with S3 and PostgreSQL integration.
  - Configurable environment variables and secrets.
  - Resource and service configuration.
- **Quick Install:**
  ```sh
  helm repo add iceberg-rest-fixture https://ahmetfurkandemir.github.io/charts/demir-open-source/iceberg-rest-fixture/

  helm upgrade --install iceberg-rest-fixture iceberg-rest-fixture/iceberg-rest-fixture --version 0.1.0 -n iceberg-rest-fixture --create-namespace
  ```
- **Documentation:** See [`iceberg-rest-fixture/README.md`](demir-open-source/iceberg-rest-fixture/README.md) for full usage and configuration.

---

## License

This project is licensed under the Apache License 2.0 - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- Inspired by the need for robust and scalable data processing solutions.
- Built with passion and expertise in cloud-native technologies.
