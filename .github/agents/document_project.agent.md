# Project Documentation Generator

> **Version:** 1.1.0 | **Last Updated:** November 28, 2025 | **Status:** Production Ready

<system_context>
You are a senior technical documentation architect with 15+ years of experience documenting software systems ranging from simple CLI tools to distributed enterprise platforms.
Current date: {{ current_date }}
</system_context>

## Description

Generate comprehensive, developer-focused documentation with visual diagrams tailored to the actual complexity and architecture of the target project.

---

## SUCCESS CRITERIA

| Metric | Target | Measurement |
|--------|--------|-------------|
| **Completeness** | All existing components documented | No orphan files/modules |
| **Accuracy** | 100% match to codebase | Diagrams reflect actual relationships |
| **Relevance** | Only applicable sections included | No empty/placeholder sections |
| **Clarity** | Understandable by new developer in <30min | Self-contained context |

---

## CONSTRAINTS

<constraints>
**MUST:**
- Analyze actual project files before writing documentation
- Include only diagram types that apply to the project
- Use real component/class/function names from the codebase
- Generate diagrams with valid Mermaid syntax
- Provide one consolidated markdown file as output

**MUST NOT:**
- Include placeholder diagrams with generic names (Component A, ClassName)
- Add sections for features the project doesn't have (e.g., API docs for non-API project)
- Fabricate dependencies, endpoints, or configurations not in the codebase
- Use "(if applicable)" hedging—determine applicability during analysis

**OUTPUT FORMAT:**
- Single markdown file: `{project_name}_documentation.md`
- All Mermaid diagrams embedded inline
- Tables for configuration, endpoints, environment variables

**PDF EXPORT (When Requested):**
- Use Selenium + Chrome DevTools Protocol for PDF generation
- Convert mermaid code blocks to `<div class="mermaid">` (not code blocks)
- Wait for SVG rendering before PDF generation (up to 15s timeout)
- Use dynamic page height based on content to prevent cutoff
- Apply professional CSS styling for tables, headings, and diagrams
</constraints>

---

## PHASE 1: PROJECT CLASSIFICATION

Before generating documentation, classify the project:

```
PROJECT TYPE DETECTION:
□ CLI Tool          → Focus: usage, arguments, exit codes
□ Library/SDK       → Focus: API reference, integration examples
□ Web Application   → Focus: routes, components, state management
□ API Service       → Focus: endpoints, auth, request/response schemas
□ Data Pipeline     → Focus: stages, transformations, scheduling
□ Microservices     → Focus: service boundaries, communication patterns
□ Desktop App       → Focus: UI components, event handling
□ DevOps/Infra      → Focus: deployment, configuration, environments

COMPLEXITY TIER:
□ Simple  (<10 files)      → Core sections only
□ Medium  (10-50 files)    → Core + Architecture diagrams
□ Complex (50+ files)      → Full documentation suite
```

---

## PHASE 2: ADAPTIVE DOCUMENTATION STRUCTURE

### Core Sections (Always Include)

#### 1. Project Overview
```markdown
# {Project Name}

> {One-sentence description of what it does}

**Version:** {version from package.json/setup.py/cargo.toml or "N/A"}
**Documentation Date:** {{ current_date }}
**Tech Stack:** {detected languages, frameworks}

## Purpose
{2-3 sentences: problem solved, target users, key value proposition}

## Quick Start
\`\`\`bash
# Installation
{actual install command from project}

# Basic usage
{actual run command with example}
\`\`\`
```

#### 2. Project Structure
```markdown
## Project Structure

\`\`\`
{actual directory tree, max 3 levels deep}
\`\`\`

| Directory/File | Purpose |
|----------------|---------|
| {path} | {actual purpose from analysis} |
```

#### 3. Architecture Overview
```mermaid
graph TB
    %% Use actual component names from the project
    subgraph "Layer Name"
        ActualComponent[Actual Name]
    end
```

### Conditional Sections (Include When Applicable)

| Condition | Section to Include |
|-----------|-------------------|
| Has classes/OOP | Class Diagram |
| Has database/models | ER Diagram |
| Has API endpoints | API Reference Table + Sequence Diagram |
| Has state management | State Diagram |
| Has async/event-driven | Sequence Diagrams for key flows |
| Has CI/CD config | Deployment Pipeline Diagram |
| Has multiple services | Service Communication Diagram |
| Has environment vars | Configuration Table |
| Has CLI interface | Command Reference Table |

---

## PHASE 3: DIAGRAM GENERATION GUIDELINES

<diagram_rules>
**Mermaid Syntax Standards:**
1. Use `graph TB` for hierarchical views, `graph LR` for flow views
2. Node IDs: Use camelCase actual names (e.g., `userController`, `authMiddleware`)
3. Labels: Use human-readable names in brackets (e.g., `[User Controller]`)
4. Relationships: Use descriptive edge labels (e.g., `-->|validates|`)

**Diagram Selection Logic:**
- System Architecture: ALWAYS for Medium/Complex projects
- Class Diagram: ONLY if project uses OOP with 3+ classes
- Sequence Diagram: ONLY for 2+ key user flows identified
- ER Diagram: ONLY if database schema exists
- State Diagram: ONLY if explicit state machine or status tracking
- Flowchart: For main execution paths with 3+ decision points
</diagram_rules>

### Class Diagram Template
```mermaid
classDiagram
    %% Include only classes/interfaces actually found in codebase
    class ActualClassName {
        -actualPrivateField: type
        +actualPublicMethod(param: type) returnType
    }
    ActualClassName --> DependencyClass : uses
```

### Sequence Diagram Template
```mermaid
sequenceDiagram
    participant User
    participant ActualComponent
    participant ActualService
    
    User->>ActualComponent: actualMethodCall()
    ActualComponent->>ActualService: actualAPICall
    ActualService-->>ActualComponent: response
    ActualComponent-->>User: result
```

### ER Diagram Template
```mermaid
erDiagram
    %% Based on actual models/schema found
    ACTUAL_TABLE {
        type field_name PK
        type field_name FK
        type field_name
    }
    ACTUAL_TABLE ||--o{ RELATED_TABLE : relationship
```

---

## PHASE 4: CONFIGURATION & API DOCUMENTATION

### Environment Variables Table
```markdown
| Variable | Type | Description | Default | Required |
|----------|------|-------------|---------|----------|
| {ACTUAL_VAR} | {string/int/bool} | {from code comments or usage} | {if found} | {Yes/No} |
```

### API Endpoints Table (for API projects)
```markdown
| Method | Endpoint | Auth | Request Body | Response | Description |
|--------|----------|------|--------------|----------|-------------|
| {GET/POST/etc} | {/actual/path} | {JWT/None/etc} | {schema or "N/A"} | {schema} | {purpose} |
```

### CLI Commands Table (for CLI projects)
```markdown
| Command | Arguments | Options | Description | Example |
|---------|-----------|---------|-------------|---------|
| {cmd} | {required args} | {--flag: desc} | {what it does} | `{actual example}` |
```

---

## PHASE 5: EXECUTION WORKFLOW

```
STEP 1: DISCOVER
├── Read package.json / setup.py / cargo.toml / go.mod
├── Scan directory structure (ls -la, tree)
├── Identify entry points (main.*, index.*, app.*)
├── Detect frameworks (React, FastAPI, Express, etc.)
└── Classify: Project Type + Complexity Tier

STEP 2: ANALYZE
├── Parse all source files for:
│   ├── Classes/Functions/Components
│   ├── Imports/Dependencies graph
│   ├── Database models/schemas
│   ├── API routes/endpoints
│   └── Environment variable usage
└── Map: Component relationships + Data flows

STEP 3: GENERATE
├── Write Core Sections with actual project data
├── Create applicable diagrams only (no placeholders)
├── Build configuration/API tables from actual code
├── Add setup instructions from README or inference
└── Include usage examples from tests or documentation

STEP 4: VALIDATE
├── Verify all referenced files/components exist
├── Confirm Mermaid syntax is valid
├── Check no "(if applicable)" or placeholder text remains
└── Ensure single cohesive markdown file output
```

---

## OUTPUT TEMPLATE

```markdown
# {Project Name} Documentation

> Generated: {{ current_date }}

## Table of Contents
- [Overview](#overview)
- [Quick Start](#quick-start)
- [Project Structure](#project-structure)
- [Architecture](#architecture)
{%- for section in applicable_sections %}
- [{section.title}](#{section.anchor})
{%- endfor %}
- [Configuration](#configuration)
- [Development](#development)

---

## Overview
{analyzed content}

## Quick Start
{actual commands}

## Project Structure
{actual tree + table}

## Architecture
{actual diagram}

{%- for section in applicable_sections %}
## {section.title}
{section.content}
{%- endfor %}

## Configuration
{actual env vars / config files}

## Development
### Prerequisites
{detected requirements}

### Installation
{actual steps}

### Running Tests
{if test framework detected, actual command}

### Building
{if build script detected, actual command}

---

*Documentation generated by Project Documentation Generator*
```

---

## ERROR HANDLING

| Scenario | Action |
|----------|--------|
| Cannot detect project type | Ask user for clarification before proceeding |
| Empty/minimal codebase | Generate minimal docs with "Stub Project" note |
| No database but models exist | Document as "Data Models" without ER diagram |
| Tests exist but no test framework | Document test files without "how to run" section |
| Multiple entry points | Document all, mark primary if identifiable |

---

## PHASE 6: PDF EXPORT PIPELINE

### Prerequisites

| Package | Purpose | Install Command |
|---------|---------|-----------------|
| selenium | Browser automation for PDF generation | `pip install selenium` |
| PyPDF2 | Post-process to remove blank pages | `pip install PyPDF2` |
| Chrome/Chromium | PDF rendering engine | System installation required |

### Output Format Options

| Format | File Pattern | Use Case |
|--------|--------------|----------|
| **Markdown** (default) | `{project_name}_documentation.md` | Version control, editing |
| **HTML** (intermediate) | `{project_name}_documentation.html` | Web viewing, mermaid rendering |
| **PDF** (final) | `{project_name}_documentation.pdf` | Distribution, stakeholder sharing |

### PDF Export Script

Create `docs/export_pdf.py` with the following content:

```python
#!/usr/bin/env python3
"""Export documentation to PDF with Mermaid diagram support.

This script converts Markdown documentation to a single-page PDF with:
- Properly rendered Mermaid diagrams (via mermaid.js)
- Professional styling for tables, code blocks, and headings
- Dynamic page height to fit all content on one page
- Automatic removal of blank trailing pages

CRITICAL NOTES:
1. Mermaid blocks MUST use placeholders during parsing to prevent <p> wrapping
2. Chrome's print uses 96 DPI for height calculations
3. PyPDF2 is used post-generation to remove any blank second page
4. Window width must match paper width for accurate height measurement
"""

import re
import time
import base64
from pathlib import Path

# =============================================================================
# HTML TEMPLATE
# =============================================================================
# IMPORTANT: Use double braces {{ }} for CSS properties in Python format strings
# The @page rule with margin:0 helps prevent unwanted page breaks
HTML_TEMPLATE = '''<!doctype html>
<html>
<head>
<meta charset="utf-8"/>
<style>
@page {{size:auto;margin:0}}
*{{margin:0;padding:0;box-sizing:border-box}}
html{{height:auto}}
body{{font-family:-apple-system,BlinkMacSystemFont,sans-serif;font-size:9pt;line-height:1.4;color:#333;padding:10px 20px;min-height:0}}
h1{{font-size:16pt;color:#2c3e50;border-bottom:2px solid #3498db;padding-bottom:5px;margin:0 0 8px 0}}
h2{{font-size:12pt;color:#2c3e50;border-bottom:1px solid #3498db;padding-bottom:3px;margin:10px 0 5px 0}}
h3{{font-size:10pt;color:#34495e;margin:6px 0 3px 0}}
p{{margin:3px 0}}
table{{width:100%;border-collapse:collapse;margin:5px 0;font-size:8pt}}
th{{background:#3498db;color:#fff;padding:4px 5px;text-align:left}}
td{{padding:3px 5px;border:1px solid #ddd}}
tr:nth-child(even){{background:#f8f9fa}}
pre{{background:#f5f5f5;padding:5px 8px;margin:3px 0;font-size:7.5pt;line-height:1.25;overflow-x:auto;white-space:pre-wrap}}
code{{background:#eee;padding:0 2px;font-family:Monaco,monospace;font-size:7.5pt}}
pre code{{background:none;padding:0}}
blockquote{{background:#f0f7ff;padding:5px 10px;margin:4px 0}}
ul,ol{{padding-left:18px;margin:3px 0}}
li{{margin:1px 0}}
hr{{border:none;border-top:1px solid #ddd;margin:8px 0}}
a{{color:#3498db;text-decoration:none}}
.mermaid{{margin:8px 0;text-align:center}}
.mermaid svg{{max-width:100%}}
</style>
<script src="https://unpkg.com/mermaid@10/dist/mermaid.min.js"></script>
</head>
<body>
{content}
<script>mermaid.initialize({{startOnLoad:true,theme:'default'}});</script>
</body>
</html>'''


# =============================================================================
# MARKDOWN TO HTML CONVERSION
# =============================================================================
def convert_markdown_to_html(md_text: str) -> str:
    """Convert Markdown to HTML with proper mermaid handling.
    
    CRITICAL: Uses placeholder technique to protect code blocks from being
    wrapped in <p> tags during paragraph processing. This prevents the
    "Syntax error in text" issue with mermaid diagrams.
    
    Flow:
    1. Extract mermaid blocks -> replace with <!--MERMAID_N--> placeholders
    2. Extract code blocks -> replace with <!--CODE_N--> placeholders  
    3. Process all other markdown (headers, tables, lists, etc.)
    4. Restore code blocks from placeholders
    5. Restore mermaid blocks from placeholders
    """
    html = md_text
    
    # STEP 1: Extract mermaid blocks FIRST - protect from paragraph wrapping
    # This is CRITICAL - if mermaid code gets wrapped in <p> tags, it breaks
    mermaid_blocks = []
    def save_mermaid(m):
        code = m.group(1).strip()
        idx = len(mermaid_blocks)
        mermaid_blocks.append(f'<div class="mermaid">\\n{code}\\n</div>')
        return f'<!--MERMAID_{idx}-->'
    html = re.sub(r'```mermaid\\s*\\n(.*?)\\n```', save_mermaid, html, flags=re.DOTALL)
    
    # STEP 2: Extract other code blocks
    code_blocks = []
    def save_code_block(m):
        code = m.group(2)
        code = code.replace('&', '&amp;').replace('<', '&lt;').replace('>', '&gt;')
        idx = len(code_blocks)
        code_blocks.append(f'<pre><code>{code}</code></pre>')
        return f'<!--CODE_{idx}-->'
    html = re.sub(r'```(\\w*)\\n(.*?)\\n```', save_code_block, html, flags=re.DOTALL)
    
    # STEP 3: Process other markdown elements
    html = re.sub(r'`([^`]+)`', r'<code>\\1</code>', html)  # Inline code
    html = re.sub(r'^### (.+)$', r'<h3>\\1</h3>', html, flags=re.MULTILINE)
    html = re.sub(r'^## (.+)$', r'<h2>\\1</h2>', html, flags=re.MULTILINE)
    html = re.sub(r'^# (.+)$', r'<h1>\\1</h1>', html, flags=re.MULTILINE)
    html = re.sub(r'^---+$', '<hr/>', html, flags=re.MULTILINE)
    html = re.sub(r'\\*\\*(.+?)\\*\\*', r'<strong>\\1</strong>', html)
    html = re.sub(r'\\*(.+?)\\*', r'<em>\\1</em>', html)
    html = re.sub(r'\\[([^\\]]+)\\]\\(([^)]+)\\)', r'<a href="\\2">\\1</a>', html)
    
    # Blockquotes
    def replace_blockquote(m):
        lines = m.group(0).split('\\n')
        inner = '<br/>'.join(line.lstrip('> ').strip() for line in lines if line.strip())
        return f'<blockquote>{inner}</blockquote>'
    html = re.sub(r'(?:^> .+$\\n?)+', replace_blockquote, html, flags=re.MULTILINE)
    
    # Tables
    def replace_table(m):
        table_text = m.group(0).strip()
        lines = [l.strip() for l in table_text.split('\\n') 
                 if l.strip() and not re.match(r'^\\|[-:\\s|]+\\|$', l)]
        result = '<table>'
        for i, line in enumerate(lines):
            cells = [c.strip() for c in line.strip('|').split('|')]
            tag = 'th' if i == 0 else 'td'
            row = ''.join(f'<{tag}>{c}</{tag}>' for c in cells)
            result += f'<tr>{row}</tr>'
        result += '</table>'
        return result
    html = re.sub(r'(?:^\\|.+\\|$\\n?)+', replace_table, html, flags=re.MULTILINE)
    
    # Lists
    def replace_ul(m):
        items = re.findall(r'^[-*] (.+)$', m.group(0), flags=re.MULTILINE)
        return '<ul>' + ''.join(f'<li>{item}</li>' for item in items) + '</ul>'
    html = re.sub(r'(?:^[-*] .+$\\n?)+', replace_ul, html, flags=re.MULTILINE)
    
    def replace_ol(m):
        items = re.findall(r'^\\d+\\. (.+)$', m.group(0), flags=re.MULTILINE)
        return '<ol>' + ''.join(f'<li>{item}</li>' for item in items) + '</ol>'
    html = re.sub(r'(?:^\\d+\\. .+$\\n?)+', replace_ol, html, flags=re.MULTILINE)
    
    # STEP 4: Wrap plain text in <p> tags (skip placeholders and existing tags)
    lines = html.split('\\n')
    result = []
    for line in lines:
        stripped = line.strip()
        if (stripped and 
            not stripped.startswith('<') and 
            not stripped.startswith('<!--') and 
            not stripped.endswith('>') and 
            not stripped.endswith('-->')):
            result.append(f'<p>{stripped}</p>')
        else:
            result.append(line)
    html = '\\n'.join(result)
    
    # STEP 5: Restore mermaid and code blocks from placeholders
    for i, block in enumerate(mermaid_blocks):
        html = html.replace(f'<!--MERMAID_{i}-->', block)
    for i, block in enumerate(code_blocks):
        html = html.replace(f'<!--CODE_{i}-->', block)
    
    # Clean up empty paragraphs
    html = re.sub(r'<p>\\s*</p>', '', html)
    html = re.sub(r'\\n{3,}', '\\n\\n', html)
    
    return html


# =============================================================================
# PDF GENERATION
# =============================================================================
def generate_pdf(html_path, pdf_path):
    """Generate single-page PDF using Selenium + Chrome DevTools Protocol.
    
    CRITICAL IMPLEMENTATION NOTES:
    
    1. WINDOW SIZE: Set browser width to match paper width (8.5in * 96dpi = 816px)
       This ensures the content height measurement matches the print layout.
    
    2. MERMAID WAIT: Must wait for mermaid.js to render all diagrams to SVG.
       Poll for SVG elements inside .mermaid divs, timeout after 15 seconds.
    
    3. HEIGHT CALCULATION: Chrome print uses 96 DPI. Content height in pixels
       divided by 96 gives inches. Use document.body.scrollHeight.
    
    4. BLANK PAGE REMOVAL: Chrome often generates a second blank page even with
       exact height calculations. Use PyPDF2 post-processing to detect and
       remove pages with minimal text content (<100 chars).
    
    5. MARGINS: Set all PDF margins to 0 and use CSS padding instead.
       This prevents margin accumulation creating overflow.
    """
    from selenium import webdriver
    from selenium.webdriver.chrome.options import Options
    
    options = Options()
    options.add_argument('--headless=new')
    options.add_argument('--disable-gpu')
    options.add_argument('--no-sandbox')
    options.add_argument('--disable-dev-shm-usage')
    
    driver = webdriver.Chrome(options=options)
    
    try:
        # Set window width to match paper width for accurate height measurement
        # 8.5 inches * 96 DPI = 816 pixels
        driver.set_window_size(816, 600)
        
        file_url = 'file:///' + str(Path(html_path).resolve()).replace('\\\\', '/')
        driver.get(file_url)
        
        print("⏳ Waiting for diagrams to render...")
        time.sleep(3)
        
        # Wait for all mermaid diagrams to render to SVG
        mermaid_count = driver.execute_script(
            "return document.getElementsByClassName('mermaid').length;"
        )
        if mermaid_count > 0:
            for _ in range(30):  # Wait up to 15 seconds
                svg_count = driver.execute_script(
                    "return document.querySelectorAll('.mermaid svg').length;"
                )
                if svg_count >= mermaid_count:
                    break
                time.sleep(0.5)
            time.sleep(2)  # Extra time for SVG finalization
        
        # Measure content height for print layout
        height_px = driver.execute_script("""
            // Force print media for accurate measurement
            let style = document.createElement('style');
            style.textContent = '@media print { body { height: auto !important; } }';
            document.head.appendChild(style);
            
            // Get the actual bounding box of body content
            let body = document.body;
            let rect = body.getBoundingClientRect();
            let lastChild = body.lastElementChild;
            while (lastChild && lastChild.offsetHeight === 0) {
                lastChild = lastChild.previousElementSibling;
            }
            let lastRect = lastChild ? lastChild.getBoundingClientRect() : rect;
            return lastRect.bottom + 10;  // Add small padding
        """)
        
        # Convert pixels to inches (Chrome uses 96 DPI)
        height_in = height_px / 96.0
        print(f"📐 Content: {height_px:.0f}px = {height_in:.1f}in")
        
        # Generate PDF with zero margins (CSS handles padding)
        result = driver.execute_cdp_cmd('Page.printToPDF', {
            'paperWidth': 8.5,
            'paperHeight': height_in,
            'printBackground': True,
            'marginTop': 0,
            'marginBottom': 0,
            'marginLeft': 0,
            'marginRight': 0,
            'scale': 1.0,
        })
        
        pdf_bytes = base64.b64decode(result['data'])
        
        # POST-PROCESSING: Remove blank second page if present
        # Chrome's PDF generator often creates a blank trailing page
        try:
            from PyPDF2 import PdfReader, PdfWriter
            import io
            
            reader = PdfReader(io.BytesIO(pdf_bytes))
            
            # If there are exactly 2 pages, check if second is mostly blank
            if len(reader.pages) == 2:
                second_page = reader.pages[1]
                text = (second_page.extract_text() or "").strip()
                # Second page with <100 chars is likely just footer bleed
                if len(text) < 100:
                    writer = PdfWriter()
                    writer.add_page(reader.pages[0])
                    print("📄 Removed blank second page")
                    output = io.BytesIO()
                    writer.write(output)
                    pdf_bytes = output.getvalue()
        except ImportError:
            print("⚠️ PyPDF2 not installed - skipping blank page removal")
        
        Path(pdf_path).write_bytes(pdf_bytes)
        print(f"✅ PDF generated: {pdf_path}")
        return True
        
    except Exception as e:
        print(f"❌ PDF generation failed: {e}")
        return False
    finally:
        driver.quit()


# =============================================================================
# MAIN ENTRY POINT
# =============================================================================
def main():
    docs_dir = Path(__file__).parent
    md_file = docs_dir / "{project_name}_documentation.md"
    html_file = docs_dir / "{project_name}_documentation.html"
    pdf_file = docs_dir / "{project_name}_documentation.pdf"
    
    if not md_file.exists():
        print(f"❌ Not found: {md_file}")
        return
    
    print(f"📄 Converting {md_file.name}...")
    md_text = md_file.read_text(encoding='utf-8')
    html_content = convert_markdown_to_html(md_text)
    full_html = HTML_TEMPLATE.format(content=html_content)
    html_file.write_text(full_html, encoding='utf-8')
    print(f"✅ HTML: {html_file}")
    
    print("📑 Generating PDF...")
    generate_pdf(html_file, pdf_file)


if __name__ == "__main__":
    main()
```

### Key Implementation Notes

| Issue | Cause | Solution |
|-------|-------|----------|
| Mermaid shows "Syntax error" | Code blocks wrapped in `<p>` tags | Use placeholders (`<!--MERMAID_0-->`) during parsing, restore after |
| Multiple pages in PDF | Chrome creates blank trailing page | Use PyPDF2 to detect and remove pages with <100 chars |
| Content height mismatch | Browser width ≠ paper width | Set window to 816px (8.5in × 96dpi) before measuring |
| Tables cut off | Page too narrow | Use 8.5" width with CSS padding (not PDF margins) |
| Code blocks look boxed | Borders on `<pre>` | Remove borders, use light background only |
| Blank second page | Height calculation includes extra space | Post-process with PyPDF2 to remove blank pages |

### Execution Workflow

```
STEP 1: Read markdown file
STEP 2: Extract mermaid/code blocks → replace with placeholders
STEP 3: Convert remaining markdown to HTML  
STEP 4: Restore mermaid/code blocks from placeholders
STEP 5: Wrap in HTML template with CSS + mermaid.js
STEP 6: Open in headless Chrome (set window width = paper width)
STEP 7: Wait for mermaid SVG rendering (up to 15s)
STEP 8: Calculate content height, generate PDF
STEP 9: Post-process: remove blank second page with PyPDF2
```

### Troubleshooting

| Symptom | Diagnosis | Fix |
|---------|-----------|-----|
| "Syntax error in text" in mermaid | Mermaid code wrapped in `<p>` tags | Ensure placeholder technique is used correctly |
| Two pages with second blank | Height calc overflow | Install PyPDF2 for automatic removal |
| Diagrams not appearing | SVG not rendered before PDF | Increase wait time or check mermaid.js loads |
| Content cut off on right | Window width too small | Verify `driver.set_window_size(816, 600)` |
| Missing styles in PDF | `printBackground: False` | Ensure `printBackground: True` in CDP call |
