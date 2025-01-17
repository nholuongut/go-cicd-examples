# CI/CD Workflows for Go Application using GitHub Actions

![](https://i.imgur.com/waxVImv.png)
### [View all Roadmaps](https://github.com/nholuongut/all-roadmaps) &nbsp;&middot;&nbsp; [Best Practices](https://github.com/nholuongut/all-roadmaps/blob/main/public/best-practices/) &nbsp;&middot;&nbsp; [Questions](https://www.linkedin.com/in/nholuong/)

![GitHub language count](https://img.shields.io/github/languages/count/ashleymichaelwilliams/aws-sandbox) ![GitHub top language](https://img.shields.io/github/languages/top/ashleymichaelwilliams/aws-sandbox)<br>
![GitHub Actions](https://img.shields.io/badge/github%20actions-%232671E5.svg?style=for-the-badge&logo=githubactions&logoColor=white) ![AquaSec](https://img.shields.io/badge/aqua-%231904DA.svg?style=for-the-badge&logo=aqua&logoColor=#0018A8) !
![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white) ![Shell Script](https://img.shields.io/badge/shell_script-%23121011.svg?style=for-the-badge&logo=gnu-bash&logoColor=white) ![Terraform](https://img.shields.io/badge/terraform-%235835CC.svg?style=for-the-badge&logo=terraform&logoColor=white)
<br>

This repository contains three examples of CI/CD workflows for a Go application using GitHub Actions. Each workflow performs a set of steps, such as testing, linting, building, and deploying the application. You can choose the workflow that suits your requirements and modify it as per your needs.

## Workflow 1: Simple CI/CD Workflow with Go Test and Docker

This workflow performs the following steps:

1. Checks out the latest code from the `main` branch
2. Builds the Docker image of the Go application
3. Runs Go tests using `go test`
4. If the tests pass, pushes the Docker image to a Docker registry.

Here is the GitHub Actions workflow file:

```yaml
name: CI/CD Workflow

on:
  push:
    branches: [main]

jobs:
  build-and-test:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout code
      uses: actions/checkout@v2

    - name: Setup Go environment
      uses: actions/setup-go@v2
      with:
        go-version: '1.20'

    - name: Build and test
      run: |
        docker build -t my-go-app .
        go test ./...

    - name: Publish Docker image
      if: success()
      uses: docker/build-push-action@v2
      with:
        context: .
        push: true
        tags: my-go-app:latest
```

## Workflow 2: Advanced CI/CD Workflow with Code Coverage and Deployment

This workflow performs the following steps:

1. Checks out the latest code from the main branch.
2. Sets up the Go environment and installs dependencies
3. Runs Go tests with code coverage using go test
4. Uploads code coverage results to Codecov
5. Builds and pushes the Docker image to a Docker registry
6. Deploys the Docker image to a Kubernetes cluster using Helm

Here is the GitHub Actions workflow file:

```yaml
name: CI/CD Workflow

on:
  push:
    branches: [main]

jobs:
  test-and-deploy:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout code
      uses: actions/checkout@v2

    - name: Setup Go environment
      uses: actions/setup-go@v2
      with:
        go-version: '1.20'

    - name: Install dependencies
      run: go mod download

    - name: Run tests with coverage
      run: |
        go test -v -race -coverprofile=coverage.out ./...
        go tool cover -html=coverage.out -o coverage.html

    - name: Upload code coverage to Codecov
      uses: codecov/codecov-action@v2
      with:
        token: ${{ secrets.CODECOV_TOKEN }}

    - name: Build and push Docker image
      uses: docker/build-push-action@v2
      with:
        context: .
        push: true
        tags: my-go-app:latest

    - name: Deploy to Kubernetes with Helm
      uses: azure/k8s-deploy@v1
      with:
        method: helm
        helm-version: '3.2.4'
        namespace: my-go-app
        chart: ./helm/my-go-app
        set: image.tag=latest
        kubeconfig: ${{ secrets.KUBECONFIG }}
```

Note: The second workflow assumes that you are using Codecov for code coverage and Kubernetes with Helm for deployment. You will need to provide the necessary values for CODECOV_TOKEN and KUBECONFIG secrets in your repository.

Workflow 3: CI/CD Workflow with Linting and Integration Tests
This workflow performs the following steps:

Checks out the latest code from the main branch
Runs Go linter using golangci-lint
Builds and runs integration tests on the Go application
If the tests pass, builds and pushes the Docker image to a Docker registry.
Here is the GitHub Actions workflow file:

```yaml
name: CI/CD Workflow

on:
  push:
    branches: [main]

jobs:
  build-and-test:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout code
      uses: actions/checkout@v2

    - name: Setup Go environment
      uses: actions/setup-go@v2
      with:
        go-version: '1.20'

    - name: Lint code
      uses: golangci/golangci-lint-action@v2
      with:
        args: ['run', '--enable-all']

    - name: Build and test
      run: |
        go build -o my-go-app .
        go test ./integration_tests/...

    - name: Publish Docker image
      if: success()
      uses: docker/build-push-action@v2
      with:
        context: .
        push: true
        tags: my-go-app:latest
```

Note: In this example, we are using golangci-lint for linting and integration_tests directory for integration tests. You can modify the linting and testing steps based on your requirements. Also, ensure that you have a Dockerfile in the root directory of your Go application.

I'm are always open to your feedback.  Please contact as bellow information:
### [Contact ]
* [Name: nho Luong]
* [Skype](luongutnho_skype)
* [Github](https://github.com/nholuongut/)
* [Linkedin](https://www.linkedin.com/in/nholuong/)
* [Email Address](luongutnho@hotmail.com)

![](https://i.imgur.com/waxVImv.png)
![](bitfield.png)
[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/nholuong)

# License
* Nho Luong (c). All Rights Reserved.
