# GitLab AnyBadge Creator

## What does it do?

Use it to create your own badge for showing in README file or project head.

## Requirements

You only need a GitLab CI pipeline in your project

## Usage

1. Include the YAML file as proposed in 
```yaml
include:
  - remote: 'https://git.spooner.io/ci-templates/gitlab-anybadge-creator/-/raw/main/anybadges.yml'
``` 
1. Use the prepared `"Create Badge"` job adjust your code into the `script` part. See [Examples](#Examples)
1. Add the badge to your README with e.g. `[![Label](https://example.gitlab.com/<project-path>/-/jobs/artifacts/<ref>/raw/badges/<badge-filename>.svg?job=Create+Badge)](<link-to-head-when-clicking>)`

## Examples

### Show latest tag

Code in your .gitlab-ci.yml:

```yaml
include:
  - remote: 'https://git.spooner.io/spooner-web/gitlab-anybadge-creator/-/raw/main/anybadges.yml'

stages:
  - ...
  - badges
  - ...

"Create Badge":
  stage: badges
  script:
    - latest_version=$(git describe --abbrev=0)
    - anybadge -l "Latest Version" -v $latest_version -f latestVersion.svg -c blue
```

README.md file:

`[![Latest Version](https://example.gitlab.org/<project-path>/-/jobs/artifacts/<ref>/raw/badges/<badge-filename>.svg?job=Create+Badge)](https://example.gitlab.org/<project-path>/-/tags)`
