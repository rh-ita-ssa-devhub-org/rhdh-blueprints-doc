# API Reference

Reference documentation for RHDH Blueprints APIs and integrations.

## Scaffolder API

### Endpoints

#### List Templates

```
GET /api/scaffolder/v2/templates
```

Returns all available templates.

**Response:**

```json
{
  "items": [
    {
      "apiVersion": "scaffolder.backstage.io/v1beta3",
      "kind": "Template",
      "metadata": {
        "name": "template-name",
        "title": "Template Title",
        "description": "Template description"
      },
      "spec": {
        "owner": "team-name",
        "type": "service"
      }
    }
  ]
}
```

#### Get Template

```
GET /api/scaffolder/v2/templates/{namespace}/{kind}/{name}
```

Returns a specific template.

**Parameters:**

| Parameter | Type | Description |
|-----------|------|-------------|
| `namespace` | string | Entity namespace (default: `default`) |
| `kind` | string | Entity kind (`Template`) |
| `name` | string | Template name |

#### Execute Template

```
POST /api/scaffolder/v2/tasks
```

Executes a template to scaffold a new component.

**Request Body:**

```json
{
  "templateRef": "template:default/my-template",
  "values": {
    "name": "my-component",
    "description": "Component description",
    "owner": "team-platform"
  }
}
```

**Response:**

```json
{
  "id": "task-uuid",
  "status": "processing",
  "createdAt": "2024-01-15T10:30:00Z"
}
```

#### Get Task Status

```
GET /api/scaffolder/v2/tasks/{taskId}
```

Returns the status of a scaffolding task.

**Response:**

```json
{
  "id": "task-uuid",
  "status": "completed",
  "output": {
    "links": [
      {
        "title": "Repository",
        "url": "https://github.com/org/repo"
      }
    ]
  },
  "steps": [
    {
      "id": "fetch",
      "name": "Fetch Template",
      "status": "completed"
    }
  ]
}
```

### Task Statuses

| Status | Description |
|--------|-------------|
| `open` | Task is queued |
| `processing` | Task is running |
| `completed` | Task finished successfully |
| `failed` | Task encountered an error |
| `cancelled` | Task was cancelled |

## Template Expression Language

### Variables

Access parameter values:

```
${{ parameters.name }}
${{ parameters.config.nested.value }}
```

### Step Outputs

Access outputs from previous steps:

```
${{ steps['step-id'].output.propertyName }}
```

### Built-in Functions

#### String Functions

```yaml
# Convert to lowercase
${{ parameters.name | lower }}

# Convert to uppercase  
${{ parameters.name | upper }}

# Replace characters
${{ parameters.name | replace("-", "_") }}

# Truncate
${{ parameters.description | truncate(100) }}
```

#### Path Functions

```yaml
# Parse repository URL
${{ parameters.repoUrl | parseRepoUrl }}

# Result: { host, owner, repo }
```

### Conditionals

```yaml
${{ parameters.includeTests and "with-tests" or "no-tests" }}
```

## Catalog Integration

### Register Entity

After scaffolding, register the entity in the catalog:

```yaml
- id: register
  action: catalog:register
  input:
    repoContentsUrl: ${{ steps['publish'].output.repoContentsUrl }}
    catalogInfoPath: /catalog-info.yaml
```

### Entity Reference Format

```
[<kind>:][<namespace>/]<name>
```

**Examples:**

- `component:default/my-service`
- `template:default/spring-boot`
- `group:platform-team`

## Webhook Events

### Task Events

| Event | Description |
|-------|-------------|
| `scaffolder.task.created` | New task started |
| `scaffolder.task.completed` | Task finished successfully |
| `scaffolder.task.failed` | Task encountered error |

### Event Payload

```json
{
  "event": "scaffolder.task.completed",
  "taskId": "task-uuid",
  "templateRef": "template:default/my-template",
  "createdBy": "user:default/username",
  "timestamp": "2024-01-15T10:35:00Z",
  "output": {
    "entityRef": "component:default/my-component"
  }
}
```

## Error Codes

| Code | Description | Resolution |
|------|-------------|------------|
| `TEMPLATE_NOT_FOUND` | Template doesn't exist | Verify template name and namespace |
| `INVALID_PARAMETERS` | Parameter validation failed | Check parameter requirements |
| `ACTION_FAILED` | Step action failed | Review action configuration |
| `PUBLISH_FAILED` | Repository creation failed | Check credentials and permissions |
| `REGISTER_FAILED` | Catalog registration failed | Verify catalog-info.yaml |


