# Tag Images with Custom Tag

This GitHub Action tags existing container images with a custom tag and pushes them back to a registry.


## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `images` | Images to tag | ✅ | |
| `tag` | The tag to apply (e.g., qa, staging, prod) | ✅ | |
| `registry` | Registry URL to push images to (e.g., registry.cern.ch, docker.io) | ❌ | `docker.io` |
| `registry-username` | Username for registry login | ✅ | |
| `registry-password` | Password/token for registry login | ✅ | |

## Usage

### Docker Hub (Default Registry)

```yaml
- name: Tag images for QA
 uses: cern-sis/gh-workflows/.github/actions/tag-images@vX.X
  with:
    images: |
      inspirehep/hep@sha256:abc123...
      inspirehep/ui@sha256:def456...
    tag: qa
    registry-username: ${{ secrets.DOCKERHUB_USERNAME }}
    registry-password: ${{ secrets.DOCKERHUB_TOKEN }}
```

### Custom Registry (e.g., CERN)

```yaml
- name: Tag with environment label
  uses: cern-sis/gh-workflows/.github/actions/tag-images@vX.X
  with:
    images: |
      registry.cern.ch/cern-sis/inspire/renderer@${{ steps.build.outputs.digest }}
    tag: qa
    registry: registry.cern.ch
    registry-username: ${{ secrets.REGISTRY_USERNAME }}
    registry-password: ${{ secrets.REGISTRY_PASSWORD }}
```
