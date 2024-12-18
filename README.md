# Build & Push Docker Image to Amazon ECR 🐳

## About

The Action builds and pushes a docker image with the specified image tag.

If the specified ECR Repository does not exist, create repository.

## Simple Example of Usage

```yml
- name: Configure AWS credentials 🔑
  uses: aws-actions/configure-aws-credentials@main
  with:
    role-to-assume: ${{ vars.AWS_ROLE_ARN }}
    aws-region: ${{ vars.AWS_REGION }}

- name: Build & Push Docker Image 🐳
  id: image
  uses: deploy-actions/build-push-ecr@main
  with:
    Name: simple-api
    Tags: v1.0.0 latest
    Path: ./app
    Dockerfile: ./app/Dockerfile_lambda

- name: Deploy Lambda Function ƛ
  id: lambda
  uses: deploy-actions/lambda-api@v1
  with:
    Name: simple-api
    ImageUri: ${{ steps.image.outputs.ImageUri }}
```

## Options

| Name       | Description                                                          | Mandatory | Default    |
| ---------- | -------------------------------------------------------------------- | --------- | ---------- |
| Name       | ECR Repository Name                                                  | ✅        |            |
| Tags       | Docker Image Tags                                                    |           |            |
| Path       | Relative Path of Dockerfile, relative to the github repository root. |           | .          |
| Dockerfile | Dockerfile Name                                                      |           | Dockerfile |

## Outputs

| Name     | Description                                    | Optional |
| -------- | ---------------------------------------------- | -------- |
| ImageUri | Image Uri of of the most recently pushed image | ✅       |
