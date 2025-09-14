# Apache Ranger Helm Chart

[![Artifact Hub](https://img.shields.io/endpoint?url=https://artifacthub.io/badge/repository/apache-ranger)](https://artifacthub.io/packages/helm/apache-ranger/apache-ranger)

![](https://ranger.apache.org/ranger-logo.svg)

This Helm chart deploys [Apache Ranger](https://ranger.apache.org/) with a Bitnami PostgreSQL dependency on Kubernetes. It is designed for easy configuration, production readiness, and extensibility.

---

## Features

- **Deploys Apache Ranger Admin** as a Kubernetes Deployment
- **Bitnami PostgreSQL** as a subchart for metadata storage
- **Configurable resources, service types, and persistent storage**
- **Customizable admin password and database credentials**
- **ConfigMap-based configuration for `install.properties`**
- **Best practices for labels, naming, and maintainability**
- **Developer and project info displayed after install**

---

## Prerequisites

- Kubernetes 1.19+
- Helm 3.x
- PersistentVolume provisioner (for PostgreSQL persistence)
- (Optional) Ingress controller for external access

---

## Installing the Chart

```sh
helm repo add apache-ranger https://ahmetfurkandemir.github.io/charts/demir-open-source/apache-ranger/

helm upgrade --install apache-ranger apache-ranger/apache-ranger --version 0.1.0 -n apache-ranger --create-namespace
```
---

## Configuration

All configuration is done via `values.yaml`. Below are the most important options:

### Apache Ranger

```yaml
replicaCount: 1

image:
  repository: apache/ranger
  tag: "2.7.0"
  pullPolicy: IfNotPresent

ranger:
  adminPassword: "admin123"
```

### Service

```yaml
service:
  type: ClusterIP # or LoadBalancer, NodePort
  port: 6080
  externalIPs: []
```

### Resources

```yaml
resources:
  limits:
    cpu: 500m
    memory: 1024Mi
  requests:
    cpu: 250m
    memory: 512Mi
```

### PostgreSQL (Bitnami Subchart)

```yaml
postgresql:
  enabled: true
  auth:
    postgresPassword: postgrespass
    username: ranger
    password: rangerpass
    database: rangerdb
  primary:
    service:
      type: ClusterIP # or LoadBalancer, NodePort
      port: 5432
      externalIPs: []
    resources:
      limits:
        cpu: 500m
        memory: 1024Mi
      requests:
        cpu: 250m
        memory: 512Mi
    persistence:
      enabled: true
      storageClass: "" # Use default storage class
      size: 8Gi
      accessModes:
        - ReadWriteOnce
```

---

## Configuration Files

- **install.properties** are generated as ConfigMaps and mounted into the Ranger container.
- Database and admin credentials are templated from `values.yaml`.

---

## Accessing Ranger

- By default, the service is `ClusterIP`. For external access, set `service.type` to `NodePort` or `LoadBalancer`.
- Example (NodePort):
  - Set `service.type: NodePort` and `service.nodePort: 30080`
  - Access via `http://<node-ip>:30080`

- For quick testing, use port-forward:
  ```sh
  kubectl port-forward svc/apache-ranger-apache-ranger 6080:6080 -n ranger
  ```
  Then visit [http://localhost:6080](http://localhost:6080)

---

## Default Credentials

- **Username:** `admin`
- **Password:** as set in `values.yaml` (`ranger.adminPassword`)

---

## Uninstalling

```sh
helm uninstall apache-ranger -n apache-ranger
```

---

## Developer & Project Info

- **Developer:** Ahmet Furkan Demir
- **Website:** [https://ahmetfurkandemir.com](https://ahmetfurkandemir.com)

---

## License

This project is licensed under the Apache License 2.0.

---

## Support

For issues, please open an issue on this repository or contact the developer via the website above.

---