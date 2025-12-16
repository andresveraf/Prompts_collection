### Usage Examples

#### Basic Usage

```bash
# 1. Generate markdown documentation using the agent
# (Agent creates {project_name}_documentation.md)

# 2. Convert to professional HTML
python docs/export_html.py

# 3. Open in browser
open docs/{project_name}_documentation.html
```

#### Customization

```python
# Modify color scheme in HTML_TEMPLATE
:root {
    --primary: #your-color;        # Change primary brand color
    --primary-dark: #your-dark;    # Change darker variant
}

# Adjust sidebar width
:root {
    --sidebar-width: 320px;        # Make sidebar wider
}

# Change header height
:root {
    --header-height: 80px;         # Make header taller
}
```

#### Integration with CI/CD

```yaml
# .github/workflows/docs.yml
name: Generate Documentation

on:
  push:
    branches: [main]

jobs:
  docs:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-python@v4
        with:
          python-version: '3.11'
      - name: Generate Documentation
        run: |
          # Run documentation agent
          # python generate_docs.py
          # Convert to HTML
          python docs/export_html.py
      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./docs
```

### Best Practices

| Practice | Rationale | Example |
|----------|-----------|---------|
| **Version Control** | Track changes to markdown, not HTML | `.gitignore` HTML files, commit markdown |
| **Regenerate HTML** | Always regenerate from markdown source | Automate with pre-commit hooks |
| **Test Mermaid Syntax** | Validate diagrams before publishing | Use Mermaid Live Editor |
| **Optimize Images** | Use SVG for diagrams, optimize PNGs | Keep total size < 10MB |
| **Mobile Testing** | Check responsive behavior | Test on 320px, 768px, 1024px widths |
| **Accessibility** | Use semantic HTML, ARIA labels | Run Lighthouse audit |

### Troubleshooting

| Symptom | Diagnosis | Fix |
|---------|-----------|-----|
| Mermaid diagrams not rendering | JavaScript not loading | Check internet connection, mermaid.js CDN |
| Navigation not working | Missing IDs on headers | Ensure `generate_toc()` creates proper anchors |
| Sidebar overlaps content | Wrong margin calculation | Adjust `--sidebar-width` in CSS |
| Copy button not appearing | JavaScript error | Check browser console for errors |
| Mobile layout broken | Viewport meta tag missing | Ensure `<meta name="viewport">` is present |
| Slow page load | Too many diagrams | Consider lazy loading for large docs |

---

## EXECUTION WORKFLOW SUMMARY

```
┌─────────────────────────────────────────────────────────────┐
│ DOCUMENTATION GENERATION WORKFLOW                           │
└─────────────────────────────────────────────────────────────┘

PHASE 1: ANALYZE PROJECT
├─ Scan directory structure
├─ Identify tech stack & frameworks  
├─ Classify project type & complexity
└─ Extract metadata (version, dependencies)

PHASE 2: GENERATE MARKDOWN
├─ Create documentation structure
├─ Generate applicable diagrams (Mermaid)
├─ Document APIs, configs, CLI commands
└─ Write: {project_name}_documentation.md

PHASE 3: CONVERT TO HTML
├─ Run: python docs/export_html.py
├─ Parse markdown → HTML with placeholders
├─ Generate table of contents
├─ Inject professional CSS & JavaScript
└─ Output: {project_name}_documentation.html

PHASE 4: DEPLOY & SHARE
├─ Open in browser for review
├─ Deploy to GitHub Pages (optional)
└─ Share HTML file with stakeholders
```

---

*Documentation Agent v1.2.0 - Professional HTML Export Edition*
