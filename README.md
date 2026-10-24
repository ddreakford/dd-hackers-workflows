# dd-hackers-workflows

Reusable CloudBees Unify workflows for the `dd-hackers-*` components.

## container-build-publish.yaml

Builds a component's container image with kaniko and pushes it to Docker Hub as
`docker.io/<DOCKERHUB_NAMESPACE>/<appName>:<versionStart>-<cloudbees.version>`.

Inputs:

| Input          | Required | Default | Description                                 |
| -------------- | -------- | ------- | ------------------------------------------- |
| `appName`      | yes      |         | Image (Docker Hub repository) name          |
| `versionStart` | no       | `3.0`   | Prefix for the image tag                    |
| `repo`         | yes      |         | `owner/name` of the repository to build     |

Callers must pass `vars: inherit` and `secrets: inherit`, and the following must
be defined in Unify:

| Name                  | Kind     | Description                                   |
| --------------------- | -------- | --------------------------------------------- |
| `DOCKERHUB_NAMESPACE` | variable | Docker Hub user or organization to push to    |
| `DOCKERHUB_USERNAME`  | secret   | Docker Hub user that authenticates the push   |
| `DOCKERHUB_TOKEN`     | secret   | Docker Hub access token with write permission |

Example:

```yaml
  build:
    uses: ddreakford/dd-hackers-workflows/container-build-publish.yaml
    vars: inherit
    secrets: inherit
    with:
      appName: hackers-auth
      versionStart: "2.0"
      repo: ddreakford/dd-hackers-auth
```
