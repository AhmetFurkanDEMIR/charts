# iceberg-rest-fixture Helm Chart

![](https://iceberg.apache.org/assets/images/Iceberg-logo.svg)

This Helm chart deploys the **Iceberg REST Fixture** application along with an optional PostgreSQL dependency. The chart is designed for Kubernetes environments and supports S3-compatible storage backends.

---

## Features

- Deploys the [ahmetfurkandemir/iceberg-rest-fixture-postgresql](https://hub.docker.com/r/ahmetfurkandemir/iceberg-rest-fixture-postgresql) container.
- Configurable S3 and Iceberg catalog environment variables.
- Optional embedded PostgreSQL database (with persistent storage).
- Resource requests and limits for both application and database.
- Secrets support for S3 credentials.

---

## Installation

```sh
helm repo add iceberg-rest-fixture https://ahmetfurkandemir.github.io/charts/demir-open-source/iceberg-rest-fixture/

helm upgrade --install iceberg-rest-fixture iceberg-rest-fixture/iceberg-rest --version 0.0.1 -n iceberg-rest-fixture --create-namespace
```

---

## Configuration

You can customize the deployment by editing the `values.yaml` or using `--set` on the command line.

### Application Settings

| Parameter                | Description                                   | Default                                  |
|--------------------------|-----------------------------------------------|------------------------------------------|
| `replicaCount`           | Number of pods                                | `1`                                      |
| `image.repository`       | Container image repository                    | `ahmetfurkandemir/iceberg-rest-fixture-postgresql` |
| `image.tag`              | Image tag                                     | `1.10.0`                                 |
| `image.pullPolicy`       | Image pull policy                             | `IfNotPresent`                           |
| `service.type`           | Service type                                  | `ClusterIP`                              |
| `service.port`           | Service port                                  | `8181`                                   |
| `resources`              | Resource requests and limits                  | See `values.yaml`                        |

### Environment Variables

Set S3 and Iceberg catalog settings via:

```yaml
env:
  secretName: s3-secrets
  values:
    AWS_REGION: us-east-1
    CATALOG_WAREHOUSE: s3://iceberg-rest/
    CATALOG_IO__IMPL: org.apache.iceberg.aws.s3.S3FileIO
    CATALOG_S3_ENDPOINT: http://minio:9000
    CATALOG_S3_PATH_STYLE_ACCESS: "true"
```

### PostgreSQL Settings

| Parameter                        | Description                | Default         |
|-----------------------------------|----------------------------|-----------------|
| `postgresql.enabled`              | Deploy PostgreSQL          | `true`          |
| `postgresql.auth.username`        | DB username                | `iceberg`       |
| `postgresql.auth.database`        | DB name                    | `iceberg`       |
| `postgresql.auth.password`        | DB user password           | `icebergpass`   |
| `postgresql.auth.postgresPassword`| Postgres superuser password| `postgrespass`  |
| `postgresql.primary.persistence.enabled` | Enable persistence | `true`          |
| `postgresql.primary.persistence.size`    | PVC size           | `8Gi`           |

---

## S3 Secrets

The chart expects a Kubernetes secret named as specified in `env.secretName` (default: `s3-secrets`) with your S3 credentials.

Example:

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: s3-secrets
type: Opaque
stringData:
  AWS_ACCESS_KEY_ID: <your-access-key>
  AWS_SECRET_ACCESS_KEY: <your-secret-key>
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