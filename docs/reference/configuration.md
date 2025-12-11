# Configuration Reference

Complete reference for RHDH Blueprints configuration options.

## Blueprint Configuration

### Template Metadata

```yaml
apiVersion: scaffolder.backstage.io/v1beta3
kind: Template
metadata:
  name: string           # Required: Unique identifier
  title: string          # Required: Display name
  description: string    # Required: Brief description
  tags:                  # Optional: Searchable tags
    - string
  annotations:           # Optional: Additional metadata
    key: value
spec:
  owner: string          # Required: Owning team/user
  type: string           # Required: Component type
```

### Supported Types

| Type | Description |
|------|-------------|
| `service` | Backend service or API |
| `website` | Frontend application |
| `library` | Shared library or package |
| `documentation` | Documentation site |
| `other` | Other component types |

## Parameter Configuration

### Basic Parameter

```yaml
parameters:
  - title: Section Title
    description: Section description
    required:
      - paramName
    properties:
      paramName:
        title: Display Name
        type: string
        description: Help text
        default: defaultValue
```

### Parameter Types

| Type | Description | Example |
|------|-------------|---------|
| `string` | Text input | Names, descriptions |
| `number` | Numeric value | Port numbers, counts |
| `boolean` | True/false toggle | Feature flags |
| `array` | List of values | Tags, dependencies |
| `object` | Complex structure | Nested configuration |

### UI Components

```yaml
properties:
  # Standard text input
  name:
    type: string
    ui:autofocus: true
    ui:placeholder: Enter name

  # Repository picker
  repoUrl:
    type: string
    ui:field: RepoUrlPicker
    ui:options:
      allowedHosts:
        - github.com
        - gitlab.com

  # Owner picker
  owner:
    type: string
    ui:field: OwnerPicker
    ui:options:
      catalogFilter:
        kind: [Group, User]

  # Entity picker
  system:
    type: string
    ui:field: EntityPicker
    ui:options:
      catalogFilter:
        kind: System
```

### Validation

```yaml
properties:
  name:
    type: string
    minLength: 3
    maxLength: 50
    pattern: '^[a-z0-9-]+$'

  port:
    type: number
    minimum: 1024
    maximum: 65535

  email:
    type: string
    format: email
```

## Step Configuration

### Available Actions

#### fetch:template

```yaml
- id: fetch
  name: Fetch Template
  action: fetch:template
  input:
    url: ./skeleton
    targetPath: ./output
    values:
      name: ${{ parameters.name }}
    templateFileExtension: .njk
```

#### publish:github

```yaml
- id: publish
  name: Publish to GitHub
  action: publish:github
  input:
    allowedHosts:
      - github.com
    repoUrl: ${{ parameters.repoUrl }}
    description: ${{ parameters.description }}
    defaultBranch: main
    protectDefaultBranch: true
    repoVisibility: private
```

#### publish:gitlab

```yaml
- id: publish
  name: Publish to GitLab
  action: publish:gitlab
  input:
    allowedHosts:
      - gitlab.com
    repoUrl: ${{ parameters.repoUrl }}
    defaultBranch: main
    repoVisibility: internal
```

#### catalog:register

```yaml
- id: register
  name: Register Component
  action: catalog:register
  input:
    repoContentsUrl: ${{ steps['publish'].output.repoContentsUrl }}
    catalogInfoPath: /catalog-info.yaml
```

## Output Configuration

```yaml
output:
  links:
    - title: Repository
      url: ${{ steps['publish'].output.remoteUrl }}
    - title: Open in Catalog
      icon: catalog
      entityRef: ${{ steps['register'].output.entityRef }}
  text:
    - title: Instructions
      content: |
        ## Next Steps
        1. Clone the repository
        2. Install dependencies
        3. Start developing
```

## Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `SCAFFOLDER_DEFAULT_AUTHOR` | Default commit author | `Scaffolder` |
| `SCAFFOLDER_DEFAULT_BRANCH` | Default branch name | `main` |

## Conditional Logic

```yaml
steps:
  - id: conditional-step
    name: Conditional Step
    if: ${{ parameters.includeFeature === true }}
    action: fetch:template
    input:
      url: ./optional-feature
```


