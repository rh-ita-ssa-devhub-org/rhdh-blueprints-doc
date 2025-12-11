# Using Blueprints

This guide covers how to effectively use RHDH Blueprints in your workflow.

## Discovering Blueprints

### Browse the Catalog

1. Navigate to the **Create** page in RHDH
2. Use filters to narrow down options:
   - **Type**: Service, website, library, etc.
   - **Tags**: Technology, team, purpose
   - **Owner**: Maintaining team

### Search by Keywords

Use the search functionality to find blueprints by:

- Name or title
- Description keywords
- Technology stack
- Tags

## Using a Blueprint

### Step 1: Select a Blueprint

Click on a blueprint card to view its details:

- Description and purpose
- Required parameters
- Expected outputs
- Owner and support information

### Step 2: Fill Parameters

Complete the required fields:

!!! warning "Important"
    Some parameters may have validation rules. Ensure your inputs meet the requirements.

**Common Parameters:**

| Field | Description | Example |
|-------|-------------|---------|
| Name | Component identifier | `my-service` |
| Description | Brief summary | `User authentication service` |
| Owner | Responsible team | `team-auth` |
| Repository | Code location | `github.com/org/repo` |

### Step 3: Review and Create

1. Review your inputs on the summary page
2. Click **Create** to start scaffolding
3. Monitor the progress in the task view

### Step 4: Access Your Resources

After completion, you'll receive:

- **Repository link**: Access your new codebase
- **Catalog entry**: View in Backstage catalog
- **Documentation**: TechDocs for your component

## Working with Created Projects

### Initial Setup

```bash
# Clone the repository
git clone <repository-url>
cd <project-name>

# Install dependencies
npm install  # or your package manager

# Start development
npm run dev
```

### Customization

After scaffolding, customize your project:

1. Update `README.md` with project-specific information
2. Modify configuration files as needed
3. Add your business logic
4. Update the `catalog-info.yaml` if necessary

## Troubleshooting

### Common Issues

??? question "Blueprint not appearing in catalog"
    - Check that the blueprint is registered in the catalog
    - Verify your permissions to access the blueprint
    - Ensure the blueprint YAML is valid

??? question "Scaffolding fails"
    - Review error messages in the task log
    - Verify all required parameters are provided
    - Check repository permissions

??? question "Missing files in output"
    - Confirm the skeleton directory is complete
    - Check for template syntax errors
    - Review the fetch action configuration

## Best Practices

1. **Read the documentation**: Each blueprint includes usage notes
2. **Use meaningful names**: Follow naming conventions
3. **Complete all fields**: Even optional ones improve discoverability
4. **Update after creation**: Keep your component information current


