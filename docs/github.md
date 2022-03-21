# Github Actions Templates

This project contains all Github Actions templates. To make use of the repository, fork this repository and modify the `env` and `trigger` sections of each template to meet the needs of your application or repository.

- [Workflow Templates](#workflow-templates)
  - [Docker Build Push](#docker-build-push)
  - [Helm Deploy](#helm-deploy)
  - [Owasp Scan](#owasp-scan)
  - [Trivy Scan](#trivy-scan)
  - [CodeQL Scan](#codeql-scan)
  - [Sonar Repo Scan](#sonar-repo-scan)
  - [Sonar Maven Scan](#sonar-maven-scan)
  - [Putting it all Together](#putting-it-all-together)
- [Secrets Management](#secrets-management)
- [Workflow Triggers](#workflow-triggers)
- [Testing Framework](#testing-framework)
- [Reference](#reference)

## Prerequisites

Note: This project has been tested on *linux/arm64*, *linux/amd64*, *linux/aarch64*, and *darwin/arm64*.

1. [docker hub account](https://www.docker.com/)
2. [sonar cloud account](https://www.python.org/)
     - [Get your sonar cloud](https://developer.gov.bc.ca/SonarQube-on-OpenShift#sonarcloud)

## How to Use

1. To get started, copy one of the [workflow templates](#workflow-templates) to your own repository under `.github/workflows/<workflow_name>`.  *<workflow_name> needs to have yml or yaml as the file name extension*

2. Create any referenced secrets in **Repository Settings tab > Secrets > Actions > New repository secret**.

3. Push a change to trigger the workflow. The workflow will call the `bruce-wh-li/devsecops-tools` repository.

When a workflow is called, it is imported into the callers context, and executes as if all the logic is running locally within the repository.

## Workflow Templates

### Docker Build Push

*It creates nginx image from github repo in ./demo and docker build and push to docker hub*

```yaml
#workflow_name: test-docker-build-push.yml
name: docker-build-push
on:
  workflow_dispatch:
  push:
jobs:
  build-push:
    uses: bruce-wh-li/devsecops-tools/.github/workflows/build-push.yaml@main
    with:
      IMAGE_REGISTRY: docker.io
# your docker image url      
# example, IMAGE: gregnrobinson/bcgov-nginx-demo
#     IMAGE: <docker hub account>/bcgov-nginx-demo
      IMAGE: brucecruise/bcgov_nginx-demo
      WORKDIR: ./demo/nginx
    secrets:
      IMAGE_REGISTRY_USER: ${{ secrets.IMAGE_REGISTRY_USER }}
      IMAGE_REGISTRY_PASSWORD: ${{ secrets.IMAGE_REGISTRY_PASSWORD }}   
```

[Back to top](#github-actions-templates)

### Helm Deploy

_Need TAILSCALE API to complete the demo to allow access openshift from a github runner_

```yaml
#workflow_name: test-helm-deploy.yml
name: helm-deploy
on:
  workflow_dispatch:
  push:
jobs:
  helm-deploy:
    uses: bruce-wh-li/devsecops-tools/.github/workflows/helm-deploy.yaml@main
    with:
      ## HELM RELEASE NAME
      NAME: flask-web

      ## HELM VARIABLES
      HELM_DIR: ./demo/flask-web/helm
      VALUES_FILE: ./demo/flask-web/helm/values.yaml

      OPENSHIFT_NAMESPACE: "default"
      APP_PORT: "80"

      # Used to access Redhat Openshift on an internal IP address from a Github Runner.
      TAILSCALE: true
    secrets:
      IMAGE_REGISTRY_USER: ${{ secrets.IMAGE_REGISTRY_USER }}
      IMAGE_REGISTRY_PASSWORD: ${{ secrets.IMAGE_REGISTRY_PASSWORD }}
      OPENSHIFT_SERVER: ${{ secrets.OPENSHIFT_SERVER }}
      OPENSHIFT_TOKEN: ${{ secrets.OPENSHIFT_TOKEN }}
      TAILSCALE_API_KEY: ${{ secrets.TAILSCALE_API_KEY }}
```

[Back to top](#github-actions-templates)

### Owasp Scan

_Scan website specified in ZAP_TARGET_URL using OWASP Scan Tool_ 

```yaml
#workflow_name: test-owasp-scan.yml
name: owasp-scan
on:
  workflow_dispatch:
  push:
jobs:
  zap-owasp:
    uses: bruce-wh-li/devsecops-tools/.github/workflows/owasp-scan.yaml@main
    with:
      ZAP_SCAN_TYPE: 'base' # Accepted values are base and full.
## ZAP_TARGET_URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/
# ZAP_TARGET_URL: https://photo-sharing-web--bcb254-dev.apps.clab.devops.gov.bc.ca
# ZAP_TARGET_URL should be url that you can lawfully scan, e.g. your own project in test, dev namespace
      ZAP_TARGET_URL: http://www.itsecgames.com
      ZAP_DURATION: '2'
      ZAP_MAX_DURATION: '5'
# set ZAP_GCP_PUBLISH: to false if you don't have gcp account
      ZAP_GCP_PUBLISH: false
      ZAP_GCP_PROJECT: phronesis-310405  # Only required if ZAP_GCP_PUBLISH is TRUE
      ZAP_GCP_BUCKET: 'zap-scan-results' # Only required if ZAP_GCP_PUBLISH is TRUE
    secrets:
      GCP_SA_KEY: ${{ secrets.GCP_SA_KEY }} # Only required if ZAP_GCP_PUBLISH is TRUE
```

[Back to top](#github-actions-templates)

### Trivy Scan

_Trivy Scan the docker image specified_ 

```yaml
#workflow_name: test-trivy-scan.yml
name: trivy-scan
on:
  workflow_dispatch:
  push:
jobs:
  trivy-scan:
    uses: bruce-wh-li/devsecops-tools/.github/workflows/trivy-container.yaml@main
    with:
#     IMAGE: <docker account>/bcgov-nginx-demo
      IMAGE: brucecruise/bcgov-nginx-demo
      TAG: latest
```

[Back to top](#github-actions-templates)


### Using Trivy to scan Git repo

```yaml
#workflow_name: test-trivy-scan-gitrepo.yml
name: scan-gitrepo
on:
  push:
    branches:
      - master
  pull_request:
jobs:
  build:
    name: Build
    runs-on: ubuntu-18.04
    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Run Trivy vulnerability scanner in repo mode
        uses: aquasecurity/trivy-action@master
        with:
          scan-type: 'fs'
          ignore-unfixed: true
          format: 'sarif'
          output: 'trivy-results.sarif'
          severity: 'CRITICAL'

      - name: Upload Trivy scan results to GitHub Security tab
        uses: github/codeql-action/upload-sarif@v1
        with:
          sarif_file: 'trivy-results.sarif'
```
[Back to top](#github-actions-templates)
### CodeQL Scan

_It scan the source code of the  'python', 'javascript', 'css' in Git Repo_
_CodeQL supports [ 'cpp', 'csharp', 'go', 'java', 'javascript', 'python' ]_ 

```yaml
#workflow_name: test-codeql-scan.yml
name: codeql-scan
on:
  workflow_dispatch:
  push:
jobs:
  codeql-scan:
    uses: bruce-wh-li/devsecops-tools/.github/workflows/codeql.yaml@main
```

[Back to top](#github-actions-templates)

### Sonar Repo Scan

```yaml
#workflow_name: test-sonar-repo-scan.yml
name: sonar-repo-scan
on:
  workflow_dispatch:
  push:
jobs:
  sonar-repo-scan:
    uses: bruce-wh-li/devsecops-tools/.github/workflows/sonar-scanner.yaml@main
    with:
# Your Sonar Cloud Organization
# for example, ORG: ci-testing, bruce-ci-testing
#     ORG: <sonar_cloud_organization>
      ORG: {{dev.secretes.SONAR_ORG_KEY}}
# Your Project Key
# for example, PROJECT_KEY: bcgov-pipeline-templates, maven-test-bruce
      PROJECT_KEY: $${{dev.secretes.SONAR_PROJECT_KEY}}
      URL: https://sonarcloud.io
    secrets:
      SONAR_TOKEN: ${{ secrets.SONAR_TOKEN }}
```

[Back to top](#github-actions-templates)

### Sonar Maven Scan

```yaml
#workflow_name: test-sonar-maven-scan.yml
name: sonar-maven-scan
on:
  workflow_dispatch:
  push:
jobs:
  sonar-scan-mvn:
    uses: bruce-wh-li/devsecops-tools/.github/workflows/sonar-scanner-mvn.yaml@main
    with:
      WORKDIR: ./tekton/demo/maven-test
# Your Sonar Project Key
# for example, PROJECT_KEY: bcgov-pipeline-templates
      PROJECT_KEY: <project key>
    secrets:
      SONAR_TOKEN: ${{ secrets.SONAR_TOKEN }}
```

[Back to top](#github-actions-templates)

### Putting it all Together

You add several jobs to a single caller workflow and integrate secrurity related components with build and deploy components. Refer to the example below on how to do this.

```yaml
#workflow_name: test-helm-build-deploy-cicd.yml
name: helm-build-deploy-cicd
on:
  push:
    branches:
      - main
  workflow_dispatch:
jobs:
  codeql-scan:
    uses: bruce-wh-li/devsecops-tools/.github/workflows/codeql.yaml@main
  build-push:
    uses: bruce-wh-li/devsecops-tools/.github/workflows/build-push.yaml@main
    with:
      IMAGE_REGISTRY: docker.io
#      IMAGE: gregnrobinson/bcgov-nginx-demo
      IMAGE: brucecruise/bcgov-nginx-demo
      WORKDIR: ./demo/nginx
    secrets:
      IMAGE_REGISTRY_USER: ${{ secrets.IMAGE_REGISTRY_USER }}
      IMAGE_REGISTRY_PASSWORD: ${{ secrets.IMAGE_REGISTRY_PASSWORD }}
  trivy-image-scan:
    needs: build-push
    uses: bruce-wh-li/devsecops-tools/.github/workflows/trivy-container.yaml@main
    with:
#      IMAGE: gregnrobinson/bcgov-nginx-demo
      IMAGE: brucecruise/bcgov-nginx-demo
      TAG: latest
  sonar-repo-scan:
    uses: bruce-wh-li/devsecops-tools/.github/workflows/sonar-scanner.yaml@main
    with:
      ORG: ci-testing
      PROJECT_KEY: bcgov-pipeline-templates
      URL: https://sonarcloud.io
    secrets:
      SONAR_TOKEN: ${{ secrets.SONAR_TOKEN }}
  sonar-maven-scan:
    uses: bruce-wh-li/devsecops-tools/.github/workflows/sonar-scanner-mvn.yaml@main
    with:
      WORKDIR: ./tekton/demo/maven-test
      PROJECT_KEY: pipeline-templates
    secrets:
      SONAR_TOKEN: ${{ secrets.SONAR_TOKEN }}
  helm-deploy:
    needs: [build-push, trivy-image-scan]
    uses: bruce-wh-li/devsecops-tools/.github/workflows/helm-deploy.yaml@main
    with:
      ## DOCKER BUILD PARAMS
      NAME: flask-web

      ## HELM VARIABLES
      HELM_DIR: ./demo/flask-web/helm
      VALUES_FILE: ./demo/flask-web/helm/values.yaml

      OPENSHIFT_NAMESPACE: "default"
      APP_PORT: "80"

      # Used to access Redhat Openshift on an internal IP address from a Github Runner.
      TAILSCALE: true
    secrets:
      IMAGE_REGISTRY_USER: ${{ secrets.IMAGE_REGISTRY_USER }}
      IMAGE_REGISTRY_PASSWORD: ${{ secrets.IMAGE_REGISTRY_PASSWORD }}
      OPENSHIFT_SERVER: ${{ secrets.OPENSHIFT_SERVER }}
      OPENSHIFT_TOKEN: ${{ secrets.OPENSHIFT_TOKEN }}
      TAILSCALE_API_KEY: ${{ secrets.TAILSCALE_API_KEY }}
  owasp-scan:
    uses: bruce-wh-li/devsecops-tools/.github/workflows/owasp-scan.yaml@main
    needs: helm-deploy
    with:
      ZAP_SCAN_TYPE: 'base' # Accepted values are base and full.
      ZAP_TARGET_URL: http://www.itsecgames.com
      ZAP_DURATION: '2'
      ZAP_MAX_DURATION: '5'
      ZAP_GCP_PUBLISH: true
      ZAP_GCP_PROJECT: phronesis-310405  # Only required if ZAP_GCP_PUBLISH is TRUE
      ZAP_GCP_BUCKET: 'zap-scan-results' # Only required if ZAP_GCP_PUBLISH is TRUE
    secrets:
      GCP_SA_KEY: ${{ secrets.GCP_SA_KEY }} # Only required if ZAP_GCP_PUBLISH is TRUE
  slack-workflow-status:
    if: always()
    name: Post Workflow Status To Slack
    needs:
      - codeql-scan
      - build-push
      - trivy-image-scan
      - sonar-repo-scan
      - sonar-maven-scan
      - owasp-scan
      - helm-deploy
    runs-on: ubuntu-latest
    steps:
      - name: Slack Workflow Notification
        uses: Gamesight/slack-workflow-status@master
        with:
          # Required Input
          repo_token: ${{secrets.GITHUB_TOKEN}}
          slack_webhook_url: ${{secrets.SLACK_WEBHOOK_URL}}
          name: 'Github Workflows'
          icon_emoji: ':fire:'
          icon_url: 'https://img.icons8.com/material-outlined/96/000000/github.png'
```

## Workflow Triggers

```yaml
# Set triggers to tell the workflow when it should run...
on:
  push:
    branches:
    - main
    paths-ignore:
    - 'README.md'
    - '.pre-commit-config.yaml'
    - './github/workflows/pre-commit-check.yaml'
  workflow_dispatch:

# A schedule can be defined using cron format.
  schedule:
    # * is a special character in YAML so you have to quote this string
    - cron:  '30 5,17 * * *'

    # Layout of cron schedule.  'minute hour day(month) month day(week)'
    # Schedule option to review code at rest for possible net-new threats/CVE's
    # List of Cron Schedule Examples can be found at https://crontab.guru/examples.html
    # Top of Every Hour ie: 17:00:00. '0 * * * *'
    # Midnight Daily ie: 00:00:00. '0 0 * * *'
    # 12AM UTC --> 8PM EST. '0 0 * * *'
    # Midnight Friday. '0 0 * * FRI'
    # Once a week at midnight Sunday. '0 0 * * 0'
    # First day of the month at midnight. '0 0 1 * *'
    # Every Quarter. '0 0 1 */3 *'
    # Every 6 months. '0 0 1 */6 *'
    # Every Year. '0 0 1 1 *'
    #- cron: '0 0 * * *'
  ...
```

[Back to top](#github-actions-templates)

## Secrets Management

The following repository secrets are required depending on which template is being used. [Learn more](https://docs.github.com/en/actions/security-guides/encrypted-secrets).

| Secret Name             | Description |
| :---------------------- | :------------|
| IMAGE_REGISTRY_USER     | Registry username. Used for interacting with private image repositories.           |
| IMAGE_REGISTRY_PASSWORD | Registry password. Used for interacting with private image repositories.       |
| OPENSHIFT_SERVER        | The API endpoint of your Openshfit cluster. By default, this needs to be a publically accessible endpoint.       |
| OPENSHIFT_TOKEN         | A token that has the correct permissions to perform create deployment in OpenShift.       |
| SONAR_TOKEN             | Used when using the Sonar scanning templates.

## Testing Framework

Every Sunday, all worlflows are tested using a `workflow_call` to each workflow from the testing workflow.

[View Pipeline Run](https://github.com/bruce-wh-li/devsecops-tools/actions/runs/1707326261)

![image](https://user-images.githubusercontent.com/26353407/149749137-427a0384-cf79-4b2c-ac6d-c3c736db4714.png)

## Reference

[Workflow Syntax](https://docs.github.com/en/actions/learn-github-actions/workflow-syntax-for-github-actions)

[Workflow Triggers](https://docs.github.com/en/actions/learn-github-actions/events-that-trigger-workflows)

[Back to top](#github-actions-templates)
