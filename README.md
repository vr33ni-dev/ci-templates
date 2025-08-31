# CI-Templates

Reusable GitHub Actions workflows for this org.  
Pin to a tag (e.g. `@v1` or `@v1.0.0`) for stable, reproducible CI.

## Available workflows

### 1) GitLab Mirror (non-destructive)

Push all branches & tags from GitHub → GitLab (no deletions).

**Path:** `.github/workflows/gitlab-mirror.yml`  
**Inputs:**

- `gitlab_url` (string, required) — target GitLab repo HTTPS URL (ends with `.git`)

**Secrets:**

- `gitlab_token` (required) — GitLab token with `write_repository`

**Caller example (in your project):**

```yaml
# .github/workflows/gitlab-mirror.yml
name: Mirror to GitLab
on:
  push:
    branches: ["**"]
    tags: ["*"]

jobs:
  mirror:
    uses: vr33ni-dev/ci-templates/.github/workflows/gitlab-mirror.yml@v1
    with:
      gitlab_url: https://gitlab.com/vr33ni-personal/${{ github.event.repository.name }}.git
    secrets:
      gitlab_token: ${{ secrets.GITLAB_TOKEN }}
```
