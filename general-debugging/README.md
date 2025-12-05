# General Debugging Image

A minimal debugging image based on Ruby 3.2 Alpine with commonly used debugging tools.

## What's Included

- Ruby 3.2 (Alpine-based)
- PostgreSQL client
- cURL & wget
- Bash shell
- vim editor
- jq (JSON processor)
- netcat (network debugging)
- less (file viewer)
- git

## Prerequisites

### AWS ECR Login

Add this function to your `~/.zshrc` (or equivalent shell config):

```bash
aws_ecr_login () {
    aws ecr get-login-password --region us-east-1 --profile google | docker login --username AWS --password-stdin 808805215462.dkr.ecr.us-east-1.amazonaws.com
}
```

**Note:** Modify the `--profile google` parameter according to your AWS profile that has the necessary ECR credentials.

### Login

Before building and pushing, run:

```bash
aws_ecr_login
```

### Create ECR Repository (First Time Only)

If this is the first time pushing to this repository, you need to create it in ECR first:

```bash
aws ecr create-repository --repository-name general-debugging --region us-east-1 --profile google
```

**Note:** Modify `--profile google` to match your AWS profile. This only needs to be done once per repository.

## Build and Push

The build command varies slightly depending on your platform:

### Mac M-series / ARM

```bash
AWS_PROFILE=google docker buildx build --platform linux/amd64 -t 808805215462.dkr.ecr.us-east-1.amazonaws.com/general-debugging:latest --push .
```

### Mac Intel / Linux / Ubuntu

```bash
AWS_PROFILE=google docker build -t 808805215462.dkr.ecr.us-east-1.amazonaws.com/general-debugging:latest -f Dockerfile .
docker push 808805215462.dkr.ecr.us-east-1.amazonaws.com/general-debugging:latest
```

**Note:** 
- Modify `AWS_PROFILE=google` to match your AWS profile with ECR credentials
- `buildx` is typically needed for Mac M-series to build for `linux/amd64` platform
- Using `latest` tag means any rebuilds/updates will overwrite the same tag

