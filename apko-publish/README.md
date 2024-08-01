# APKO Publish

This action builds and publish an image with APKO given a config file and tag(s) to use.

## Usage

```yaml
- uses: distroless/actions/apko-publish@main
  with:
    # Config is the configuration file to use for the image build.
    # Optional, will use .apko.yaml without a defined one.
    config: foo.yaml
    # Tag is the tag that will be published.
    # Required.
    # Multiple tags can be supplied using a space-separated list
    # tag: ghcr.io/chainguard-dev/apko-example:latest ghcr.io/chainguard-dev/apko-example:1.2.3
    tag: ghcr.io/chainguard-dev/apko-example:latest
    # Image Refs is the path to a file where apko should emit a newline
    # delimited list of published image digests.
    # Optional, will use a temporary file when unspecified.
    image_refs: foo.images
```

## Scenarios

```yaml
steps:
- uses: distroless/actions/apko-publish@main
  id: apko
  with:
    config: nginx.yaml
    tag: ghcr.io/distroless/apko-example:nginx

- shell: bash
  run: |
    COSIGN_EXPERIMENTAL=true cosign sign ${{ steps.apko.outputs.digest }}
```
