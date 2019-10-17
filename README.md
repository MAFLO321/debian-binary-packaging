The scripts in this repo provide tooling to produce debian binary packages from the binary artifacts released in the `zrepl` repository.

# Building .deb packages

The resulting packages are put into `debs` for further processing, e.g. by aptly (see below).

## In Docker

Make sure Docker is installed and running on your system.

```bash
# Download GitHub released files into ./release
./docker_make_debs.bash
```

## On Debian

```bash
# Download GitHub released files into ./release
./ondebian_make_debs.bash amd64
./ondebian_make_debs.bash arm64
```

# Publishing in the APT repo

We use `aptly` (1.4 at the time of writing) for managing the zrepl APT repositories.
The script `aptly/import-debs.bash` imports packages in `debs` into the aptly *repo* and updates the aptly *filesystem publish* dir `aptly/root`.

The aptly config, database and GPG homedir for package signing are all in `aptly`.
`aptly/env.bash` can be sourced to get an `aptly` **alias** with properly set `-config` flag and `GNUPGHOME` environment variable.
