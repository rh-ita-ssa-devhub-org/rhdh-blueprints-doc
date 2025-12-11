# Creating Blueprints

Learn how to create custom blueprints for your organization.

## Blueprint Structure

A blueprint consists of the following components:

```
my-blueprint/
├── template.yaml      # Blueprint definition
├── skeleton/          # Template files
│   ├── catalog-info.yaml
│   ├── README.md
│   └── src/
└── docs/             # Blueprint documentation
```

## Template Definition

The `template.yaml` file defines the blueprint:

```yaml
apiVersion: scaffolder.backstage.io/v1beta3
kind: Template
metadata:
  name: my-custom-blueprint
  title: My Custom Blueprint
  description: A custom blueprint for my organization
  tags:
    - recommended
    - custom
spec:
  owner: team-platform
  type: service

  parameters:
    - title: Project Information
      required:
        - name
        - description
      properties:
        name:
          title: Name
          type: string
          description: Unique name for the component
        description:
          title: Description
          type: string
          description: Brief description of the component

    - title: Repository Configuration
      required:
        - repoUrl
      properties:
        repoUrl:
          title: Repository Location
          type: string
          ui:field: RepoUrlPicker
          ui:options:
            allowedHosts:
              - github.com

  steps:
    - id: fetch-base
      name: Fetch Base
      action: fetch:template
      input:
        url: ./skeleton
        values:
          name: ${{ parameters.name }}
          description: ${{ parameters.description }}

    - id: publish
      name: Publish
      action: publish:github
      input:
        allowedHosts:
          - github.com
        repoUrl: ${{ parameters.repoUrl }}

    - id: register
      name: Register
      action: catalog:register
      input:
        repoContentsUrl: ${{ steps['publish'].output.repoContentsUrl }}
        catalogInfoPath: '/catalog-info.yaml'

  output:
    links:
      - title: Repository
        url: ${{ steps['publish'].output.remoteUrl }}
      - title: Open in catalog
        icon: catalog
        entityRef: ${{ steps['register'].output.entityRef }}
```

## Template Variables

Use Nunjucks templating syntax in your skeleton files:

```markdown
# ${{ values.name }}

${{ values.description }}

## Getting Started

This project was created using the ${{ values.name }} blueprint.
```

## Best Practices

!!! success "Recommendations"
    1. **Keep it simple**: Start with minimal parameters
    2. **Document everything**: Include clear descriptions
    3. **Test thoroughly**: Validate with different inputs
    4. **Version control**: Track changes to blueprints
    5. **Use defaults**: Provide sensible default values

## Common Actions

| Action | Description |
|--------|-------------|
| `fetch:template` | Copy and process template files |
| `publish:github` | Create a GitHub repository |
| `publish:gitlab` | Create a GitLab repository |
| `catalog:register` | Register in Backstage catalog |
| `debug:log` | Log messages for debugging |

## Next Steps

- Review the [API Reference](../reference/api.md)
- Explore [existing blueprints](overview.md)
- Check [configuration options](../reference/configuration.md)


