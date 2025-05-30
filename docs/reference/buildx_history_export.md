# docker buildx history export

<!---MARKER_GEN_START-->
Export build records into Docker Desktop bundle

### Options

| Name                                   | Type     | Default | Description                                         |
|:---------------------------------------|:---------|:--------|:----------------------------------------------------|
| [`--all`](#all)                        | `bool`   |         | Export all build records for the builder            |
| [`--builder`](#builder)                | `string` |         | Override the configured builder instance            |
| [`-D`](#debug), [`--debug`](#debug)    | `bool`   |         | Enable debug logging                                |
| [`--finalize`](#finalize)              | `bool`   |         | Ensure build records are finalized before exporting |
| [`-o`](#output), [`--output`](#output) | `string` |         | Output file path                                    |


<!---MARKER_GEN_END-->

## Description

Export one or more build records to `.dockerbuild` archive files. These archives
contain metadata, logs, and build outputs, and can be imported into Docker
Desktop or shared across environments.

## Examples

### <a name="all"></a> Export all build records to a file (--all)

Use the `--all` flag and redirect the output:

```console
docker buildx history export --all > all-builds.dockerbuild
```

Or use the `--output` flag:

```console
docker buildx history export --all -o all-builds.dockerbuild
```

### <a name="builder"></a> Use a specific builder instance (--builder)

```console
docker buildx history export --builder builder0 ^1 -o builder0-build.dockerbuild
```

### <a name="debug"></a> Enable debug logging (--debug)

```console
docker buildx history export --debug qu2gsuo8ejqrwdfii23xkkckt -o debug-build.dockerbuild
```

### <a name="finalize"></a> Ensure build records are finalized before exporting (--finalize)

Clients can report their own traces concurrently, and not all traces may be
saved yet by the time of the export. Use the `--finalize` flag to ensure all
traces are finalized before exporting.

```console
docker buildx history export --finalize qu2gsuo8ejqrwdfii23xkkckt -o finalized-build.dockerbuild
```

### <a name="output"></a> Export a single build to a custom file (--output)

```console
docker buildx history export qu2gsuo8ejqrwdfii23xkkckt --output mybuild.dockerbuild
```

You can find build IDs by running:

```console
docker buildx history ls
```

To export two builds to separate files:

```console
# Using build IDs
docker buildx history export qu2gsuo8ejqrwdfii23xkkckt qsiifiuf1ad9pa9qvppc0z1l3 -o multi.dockerbuild

# Or using relative offsets
docker buildx history export ^1 ^2 -o multi.dockerbuild
```

Or use shell redirection:

```console
docker buildx history export ^1 > mybuild.dockerbuild
docker buildx history export ^2 > backend-build.dockerbuild
```
