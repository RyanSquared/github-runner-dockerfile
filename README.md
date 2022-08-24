# github-runner-docker
Dockerfile and build setup for running GitHub runners in Docker containers

### Usage

```
git clone -b v2.296.0 https://github.com/actions/runner
docker build -t github-runner .
docker run --detach --name=github-runner github-runner -v github-runner-config:/opt/runner/persistent https://github.com/RyanSquared/github-runner-docker <TOKEN>
```

### Additional Flags

You can pass the following to Docker to get extra functionality:

* `-v $PWD/keys.asc:/opt/keys/gpg/keys.asc`: Add PGP keys for use with
  `git verify-commit` and other commands.
* `-v $PWD/signing_keys.txt:/opt/signing_keys.txt`: Add PGP key fingerprints
  to be pulled from a keyserver, similar to above.
* `-v /var/run/docker.sock:/var/run/docker.sock`: Give access to the Docker
  runtime from inside the container, for the purpose of building new Docker
  containers. Container still needs `docker.io` installed, as it's not
  installed by default.

### Updating

The following files should be updated:

- `Dockerfile`: the RUNNER_VERSION argument
- `.github/workflows/docker-push.yaml`: the `git clone` command
- `README.md`: the usage instructions

Be sure to pull the latest version of the runner repository before building.
