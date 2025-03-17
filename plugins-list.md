# Jenkins Plugins Configuration Guide

This document provides a comprehensive list of recommended Jenkins plugins organized by category and instructions on how to configure them in your Jenkins Helm chart.

## How to Use This Guide

1. The default `values.yaml` file does not include any plugins to keep it clean.
2. To install Jenkins with plugins, you can:
   - Use the provided `valuesWithPlugins.yaml` as a starting point
   - Create your own custom values file with plugins from this list

### Using the valuesWithPlugins.yaml File

```bash
# Install Jenkins with the plugins defined in valuesWithPlugins.yaml
helm install jenkins -n jenkins -f valuesWithPlugins.yaml .

# Or merge with your own custom values
helm install jenkins -n jenkins -f values.yaml -f valuesWithPlugins.yaml -f my-custom-values.yaml .
```

## Recommended Plugins by Category

### Core Functionality

```yaml
# Core functionality
- configuration-as-code
- credentials
- credentials-binding
- git
- github
- github-branch-source
- kubernetes
- kubernetes-cli
- kubernetes-credentials
- workflow-aggregator
```

### UI and Visualization

```yaml
# UI and visualization
- blueocean
- bootstrap5-api
- htmlpublisher
- jenkins-design-language
- pipeline-rest-api
- pipeline-stage-view
```

### Pipeline and Build Tools

```yaml
# Pipeline and build tools
- pipeline-build-step
- pipeline-github-lib
- pipeline-graph-analysis
- pipeline-input-step
- pipeline-milestone-step
- pipeline-model-api
- pipeline-model-definition
- pipeline-model-extensions
- pipeline-stage-step
- pipeline-stage-tags-metadata
```

### Security and Authentication

```yaml
# Security and authentication
- antisamy-markup-formatter
- matrix-project
- github-oauth  # For GitHub authentication
- role-strategy  # For role-based access control
```

### SCM Related

```yaml
# SCM related
- git-client
- github-api
- scm-api
```

### Utility Plugins

```yaml
# Utility plugins
- cloudbees-folder
```

## Authentication Options

### GitHub OAuth Authentication

To enable GitHub OAuth authentication (SSO with GitHub), include the `github-oauth` plugin and add the securityRealm configuration in your values file:

```yaml
installPlugins:
  - github-oauth
  # Other plugins...

# IMPORTANT: Only add the securityRealm configuration when using GitHub OAuth for SSO
JCasC:
  securityRealm: |-
    github:
      clientID: "YOUR_GITHUB_CLIENT_ID"
      clientSecret: "YOUR_GITHUB_CLIENT_SECRET"
      githubApiUri: "https://api.github.com"
      githubWebUri: "https://github.com"
      oauthScopes: "read:org,user:email,repo"
```

Steps to set up GitHub OAuth:
1. Create a GitHub OAuth App in your GitHub organization or personal account
2. Set the Authorization callback URL to `https://your-jenkins-url/securityRealm/finishLogin`
3. Obtain the Client ID and Client Secret
4. Add them to your values file as shown above
5. If not using GitHub OAuth, remove the securityRealm section from your configuration

## Current Production Plugins List

Below is the current list of plugins from a production Jenkins instance:

```yaml
 - antisamy-markup-formatter
- apache-httpcomponents-client-4-api
- asm-api
- authentication-tokens
- blueocean-bitbucket-pipeline
- blueocean-commons
- blueocean-config
- blueocean-core-js
- blueocean-dashboard
- blueocean-display-url
- blueocean-events
- blueocean-git-pipeline
- blueocean-github-pipeline
- blueocean-i18n
- blueocean-jwt
- blueocean-personalization
- blueocean-pipeline-api-impl
- blueocean-pipeline-editor
- blueocean-pipeline-scm-api
- blueocean-rest-impl
- blueocean-rest
- blueocean-web
- blueocean
- bootstrap5-api
- bouncycastle-api
- branch-api
- caffeine-api
- checks-api
- cloudbees-bitbucket-branch-source
- cloudbees-folder
- commons-lang3-api
- commons-text-api
- configuration-as-code
- credentials-binding
- credentials
- display-url-api
- durable-task
- echarts-api
- favorite
- font-awesome-api
- git-client
- git
- github-api
- github-branch-source
- github-pullrequest
- github
- gson-api
- handy-uri-templates-2-api
- htmlpublisher
- instance-identity
- ionicons-api
- jackson2-api
- jakarta-activation-api
- jakarta-mail-api
- javax-activation-api
- jaxb
- jenkins-design-language
- jjwt-api
- joda-time-api
- jquery3-api
- json-api
- json-path-api
- junit
- kubernetes-cli
- kubernetes-client-api
- kubernetes-credentials-provider
- kubernetes-credentials
- kubernetes
- mailer
- matrix-project
- metrics
- mina-sshd-api-common
- mina-sshd-api-core
- okhttp-api
- pipeline-build-step
- pipeline-github-lib
- pipeline-github
- pipeline-graph-analysis
- pipeline-groovy-lib
- pipeline-input-step
- pipeline-milestone-step
- pipeline-model-api
- pipeline-model-definition
- pipeline-model-extensions
- pipeline-rest-api
- pipeline-stage-step
- pipeline-stage-tags-metadata
- pipeline-stage-view
- plain-credentials
- plugin-util-api
- prism-api
- pubsub-light
- purge-job-history
- resource-disposer
- scm-api
- script-security
- snakeyaml-api
- sse-gateway
- ssh-credentials
- structs
- token-macro
- variant
- workflow-aggregator
- workflow-api
- workflow-basic-steps
- workflow-cps
- workflow-durable-task-step
- workflow-job
- workflow-multibranch
- workflow-scm-step
- workflow-step-api
- workflow-support
- ws-cleanup
```

## Minimal Plugin Set for Basic Functionality

If you want a minimal set of plugins to get started:

```yaml
installPlugins:
  - configuration-as-code
  - credentials
  - git
  - github
  - kubernetes
  - workflow-aggregator
  - blueocean
  - github-oauth  # If using GitHub authentication
``` 