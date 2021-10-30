# Introduction
This project holds 2 dockerfiles to generate custom Azure DevOps [vsts-agent] docker images

# Getting Started
To run a VSTS agent on Ubuntu 16.04 for a specific account with a custom agent name, pool and a volume mapped agent work folder:

```
docker run \
  -e VSTS_ACCOUNT=jblprd \
  -e VSTS_TOKEN=<pat> \
  -e VSTS_AGENT='$(hostname)-agent' \
  -e VSTS_POOL=docker \
  -e VSTS_WORK='/var/vsts/$VSTS_AGENT' \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v /var/vsts:/var/vsts \
  -it microsoft/vsts-agent:ubuntu-16.04
```

### `docker` images
The derived images from `Dockerfile` & `Dockerfile.19.03` include a version of the Docker CLI and a compatible version of the Docker Compose CLI. This image cannot run most of the built-in VSTS build or release tasks but it can run tasks that invoke arbitrary Docker workloads.

These images do not run "Docker in Docker", but rather re-use the host instance of Docker. To ensure this works correctly, volume map the host's Docker socket into the container as shown above.


# Links
Below are the some important links to refer:

- [VSTS AGENT Github Project](https://github.com/microsoft/vsts-agent-docker/blob/master/README.md)
- [Docker Hub image](https://hub.docker.com/_/microsoft-azure-pipelines-vsts-agent)
