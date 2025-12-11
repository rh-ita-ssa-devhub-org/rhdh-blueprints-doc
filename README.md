# RHDH Blueprints Documentation

This repository contains the documentation for Red Hat Developer Hub (RHDH) Blueprints, built using [Backstage TechDocs](https://backstage.io/docs/features/techdocs/).

## Project Structure

```
├── catalog-info.yaml    # Backstage catalog entity definition
├── mkdocs.yml           # MkDocs configuration
├── docs/                # Documentation source files
│   ├── index.md         # Home page
│   ├── getting-started.md
│   ├── blueprints/
│   │   ├── overview.md
│   │   ├── creating.md
│   │   └── using.md
│   └── reference/
│       ├── configuration.md
│       └── api.md
└── README.md
```

## Local Development

### Prerequisites

- Python 3.8+
- Node.js 18+ (for TechDocs CLI)

### Setup

```bash
# Install techdocs-cli
npm install -g @techdocs/cli

# Install MkDocs and plugins
pip install mkdocs-techdocs-core
```

### Preview Documentation

```bash
# Generate and serve documentation locally
techdocs-cli serve
```

The documentation will be available at `http://localhost:3000`.

### Build Only

```bash
# Generate static site
techdocs-cli generate --no-docker
```

## Publishing to Backstage

1. Ensure `catalog-info.yaml` is properly configured with your repository details
2. Register this repository in your Backstage catalog
3. TechDocs will automatically build and serve the documentation

## Configuration

Update `mkdocs.yml` to customize:

- Site name and description
- Navigation structure
- MkDocs plugins and extensions
- Repository URLs

Update `catalog-info.yaml` to configure:

- Component metadata
- Ownership information
- TechDocs reference annotation

## Contributing

1. Edit or add Markdown files in the `docs/` directory
2. Update `mkdocs.yml` navigation if adding new pages
3. Preview changes locally with `techdocs-cli serve`
4. Submit a pull request

## Resources

- [Backstage TechDocs](https://backstage.io/docs/features/techdocs/)
- [MkDocs Documentation](https://www.mkdocs.org/)
- [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/)
