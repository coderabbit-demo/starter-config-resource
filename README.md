# starter-config-resource

This repository has a starter `.coderabbit.yaml` config file that will help you enable CodeRabbit features from the out of the box configuration.

## Configuration Inheritance

CodeRabbit supports a powerful **configuration inheritance** model that lets you define shared standards organization-wide while still allowing individual repositories to customize their own settings.

### How it works

You can maintain a central `coderabbit` repository in your GitHub/GitLab organization that holds a shared `.coderabbit.yaml`. Any repository that sets `inheritance: true` in its own `.coderabbit.yaml` will automatically merge settings from that central config.

**Priority order (highest → lowest):**

1. Repository `.coderabbit.yaml` (per-repo customizations)
2. Central `.coderabbit.yaml` (in your `coderabbit` repository)
3. UI settings (org/workspace)
4. CodeRabbit schema defaults

### Merge behavior

- **Objects** are deep-merged — child properties override parent properties
- **Arrays** — child items appear first, followed by unique parent items
- **Scalars** — child values always override parent values

### Setup

1. Create a repository named `coderabbit` in your GitHub/GitLab organization.
2. Add a `.coderabbit.yaml` to it with your organization-wide defaults (e.g. custom checks, security policies, path instructions).
3. In each individual repository's `.coderabbit.yaml`, add `inheritance: true` at the top — this repo's config already has this enabled.

```yaml
inheritance: true  # merges settings from the central coderabbit repo
```

Individual repos can then override only what they need (e.g. a different `profile`, additional `path_instructions`) while automatically inheriting everything else from the central config.

### Verify your resolved config

Run the following command on any pull request to see the fully resolved configuration with source annotations:

```
@coderabbitai configuration
```

This shows exactly where each setting originated in the inheritance chain.

For full details, see the [CodeRabbit configuration inheritance docs](https://docs.coderabbit.ai/configuration/configuration-inheritance).
