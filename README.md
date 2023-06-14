# Exercise: Using Woodpecker CI to build/deploy in separate pipelines

This repository shows how Woodpecker CI can be used to build and deploy
an application in separate pipelines. This can be useful if you want to
review the build before deploying it.

## Use Cases

- Moving older applications to a CI/CD pipeline that may not be trusted
  enough to deploy automatically.
- Terraform and other infrastructure as code tools that may need to be
  reviewed before being deployed to ensure that they are not going to
  cause any issues.

## CI Secrets

| Secret           | Description                         |
| ---------------- | ----------------------------------- |
| minio_bucket     | The name of the MinIO bucket to use |
| minio_access_key | The access key for the MinIO bucket |
| minio_secret_key | The secret key for the MinIO bucket |
| minio_endpoint   | The endpoint for the MinIO bucket   |

## Build pipeline

The build pipeline is triggered by pushing a commit to the repository.
It is defined in the file `build.yml`. It creates a sample text file and
pushes it up to a MinIO bucket.

## Deploy pipeline

The deploy pipeline is triggered by creating a deployment through the
woodpecker interface. It is defined in the file `deploy.yml`. It pulls
the file from the MinIO bucket and prints it to the screen.
