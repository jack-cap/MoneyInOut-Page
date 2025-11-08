# Money In & Out - Documentation

This folder contains the MkDocs documentation for Money In & Out, designed to be published as GitHub Pages.

## Quick Start

### Install Dependencies

```bash
pip install -r requirements.txt
```

### Preview Locally

```bash
mkdocs serve
```

Then open http://127.0.0.1:8000 in your browser.

### Build Site

```bash
mkdocs build
```

This creates a `site/` directory with the static website.

## Deploying to GitHub Pages

### Option 1: Automatic Deployment

```bash
mkdocs gh-deploy
```

This builds and pushes to the `gh-pages` branch automatically.

### Option 2: Manual Deployment

1. Build the site:
   ```bash
   mkdocs build
   ```

2. Push the `site/` directory to `gh-pages` branch:
   ```bash
   git subtree push --prefix ghpage/site origin gh-pages
   ```

### Option 3: GitHub Actions

Create `.github/workflows/docs.yml`:

```yaml
name: Deploy Documentation

on:
  push:
    branches:
      - main
    paths:
      - 'ghpage/**'

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Setup Python
        uses: actions/setup-python@v4
        with:
          python-version: 3.x
      
      - name: Install dependencies
        run: |
          pip install -r ghpage/requirements.txt
      
      - name: Deploy to GitHub Pages
        run: |
          cd ghpage
          mkdocs gh-deploy --force
```

## Configuration

### Update Site URL

Edit `mkdocs.yml`:

All placeholders have been updated with the correct repository information:

- **Repository**: https://github.com/jack-cap/MoneyInOut-Page
- **Site URL**: https://jack-cap.github.io/MoneyInOut-Page/
- **Support Email**: MoneyIO@thecapitalyst.com

### App Store Link

When the app is published to the App Store, update the download links in:
- `docs/index.md`
- `docs/getting-started/installation.md`
- `mkdocs.yml` (uncomment the App Store social link)

## Structure

```
ghpage/
├── mkdocs.yml              # MkDocs configuration
├── requirements.txt        # Python dependencies
├── README.md              # This file
└── docs/                  # Documentation content
    ├── index.md           # Home page
    ├── getting-started/   # Getting started guides
    ├── user-guide/        # User documentation
    ├── development/       # Developer documentation
    ├── privacy-policy.md  # Privacy policy
    ├── faq.md            # FAQ
    └── support.md        # Support information
```

## Customization

### Theme Colors

Edit `mkdocs.yml` to change colors:

```yaml
theme:
  palette:
    primary: indigo  # Change to your preferred color
    accent: indigo   # Change to your preferred color
```

Available colors: red, pink, purple, deep purple, indigo, blue, light blue, cyan, teal, green, light green, lime, yellow, amber, orange, deep orange

### Navigation

Edit the `nav` section in `mkdocs.yml` to reorganize pages.

### Add Pages

1. Create a new `.md` file in `docs/`
2. Add it to the `nav` section in `mkdocs.yml`

## Writing Documentation

### Markdown Features

MkDocs supports:

- Standard Markdown
- Code blocks with syntax highlighting
- Tables
- Admonitions (notes, warnings, tips)
- Tabs
- And more via extensions

### Admonitions

```markdown
!!! note "Optional Title"
    This is a note

!!! warning
    This is a warning

!!! tip
    This is a tip
```

### Code Blocks

````markdown
```swift
let transaction = Transaction(amount: 50.0)
```
````

### Links

```markdown
[Link text](path/to/page.md)
[External link](https://example.com)
```

## Assets

### Images

1. Create `docs/assets/` directory
2. Add images there
3. Reference in markdown:

```markdown
![Alt text](assets/image.png)
```

### App Icon

Add your app icon to `docs/assets/app-icon.png` for use in documentation.

## Testing

Before deploying:

1. **Preview locally** - Check all pages render correctly
2. **Test links** - Ensure all internal links work
3. **Check formatting** - Verify code blocks, tables, etc.
4. **Mobile view** - Test responsive design
5. **Search** - Try searching for content

## Maintenance

### Regular Updates

- Update version numbers
- Add new features to documentation
- Keep FAQ current
- Update screenshots
- Review and fix broken links

### Version Control

- Commit documentation changes
- Use meaningful commit messages
- Keep docs in sync with app versions

## Troubleshooting

### Build Errors

If `mkdocs build` fails:

1. Check YAML syntax in `mkdocs.yml`
2. Verify all referenced files exist
3. Check for broken internal links
4. Review error messages

### Deployment Issues

If `mkdocs gh-deploy` fails:

1. Ensure you have push access to repository
2. Check GitHub Pages is enabled in repo settings
3. Verify branch is set to `gh-pages`
4. Check for authentication issues

### Preview Not Working

If `mkdocs serve` fails:

1. Check port 8000 is available
2. Try different port: `mkdocs serve -a localhost:8001`
3. Verify dependencies are installed

## Resources

- [MkDocs Documentation](https://www.mkdocs.org/)
- [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/)
- [GitHub Pages Documentation](https://docs.github.com/en/pages)

## Support

For issues with this documentation:

- Open an issue on GitHub
- Email MoneyIO@thecapitalyst.com
- Check MkDocs documentation
