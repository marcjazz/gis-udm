# MKDocs to Antora Conversion and Deployment Plan

This document outlines the plan for converting the existing MKDocs site to an Antora site and deploying it to GitHub Pages.

## 1. Conversion Plan

### 1.1. `mkdocs.yml` Analysis

The `mkdocs.yml` file defines the site structure and navigation. The site is organized into three main sections:

-   **Linux Fundamentals (UCC111)**
-   **Linux Expert (UCC121)**
-   **Virtualization Fundamentals (UCC141)**

Each section corresponds to a course and contains several topics and labs. The configuration also uses the following Markdown extensions that will need to be converted to AsciiDoc syntax:

-   `admonition`
-   `codehilite`
-   `attr_list`
-   `md_in_html`
-   `shadcn.extensions.codexec`
-   `excalidraw`

### 1.2. File-by-File Mapping

The following table maps the Markdown files from the `docs/` directory to their corresponding AsciiDoc files in the `asciidocs/` directory.

| Source (docs/) | Target (asciidocs/) |
| --- | --- |
| `index.md` | `asciidocs/content/ucc111/modules/ROOT/pages/index.adoc` |
| `ucc111/index.md` | `asciidocs/content/ucc111/modules/ROOT/pages/index.adoc` |
| `ucc111/installation_and_pkg_mgnt/index.md` | `asciidocs/content/ucc111/modules/ROOT/pages/installation_and_pkg_mgnt/index.adoc` |
| `ucc111/labs/lab1.md` | `asciidocs/content/ucc111/modules/ROOT/pages/labs/lab1.adoc` |
| `ucc121/index.md` | `asciidocs/content/ucc121/modules/ROOT/pages/index.adoc` |
| `ucc121/ai_in_admin/index.md` | `asciidocs/content/ucc121/modules/ROOT/pages/ai_in_admin/index.adoc` |
| `ucc121/labs/scripting_lab1.md` | `asciidocs/content/ucc121/modules/ROOT/pages/labs/scripting_lab1.adoc` |
| `ucc121/scripting/index.md` | `asciidocs/content/ucc121/modules/ROOT/pages/scripting/index.adoc` |
| `ucc121/scripting/session1.md` | `asciidocs/content/ucc121/modules/ROOT/pages/scripting/session1.adoc` |
| `ucc121/scripting/session2.md` | `asciidocs/content/ucc121/modules/ROOT/pages/scripting/session2.adoc` |
| `ucc141/index.md` | `asciidocs/content/ucc141/modules/ROOT/pages/index.adoc` |
| `ucc141/virtualization_fundamentals/index.md` | `asciidocs/content/ucc141/modules/ROOT/pages/virtualization_fundamentals/index.adoc` |
| `ucc141/virtualization_fundamentals/session2.md` | `asciidocs/content/ucc141/modules/ROOT/pages/virtualization_fundamentals/session2.adoc` |
| `ucc141/virtualization_fundamentals/session3.md` | `asciidocs/content/ucc141/modules/ROOT/pages/virtualization_fundamentals/session3.adoc` |
| `ucc141/virtualization_fundamentals/session4.md` | `asciidocs/content/ucc141/modules/ROOT/pages/virtualization_fundamentals/session4.adoc` |
| `ucc141/virtualization_fundamentals/session5.md` | `asciidocs/content/ucc141/modules/ROOT/pages/virtualization_fundamentals/session5.adoc` |
| `ucc141/virtualization_fundamentals/session6.md` | `asciidocs/content/ucc141/modules/ROOT/pages/virtualization_fundamentals/session6.adoc` |

### 1.3. Syntax Conversion

The conversion from Markdown to AsciiDoc will require the following syntax changes:

-   **Admonitions:** Markdown admonitions (e.g., `!!! note`) will be converted to AsciiDoc admonition blocks (e.g., `[NOTE]`).
-   **Code Blocks:** Markdown code blocks will be converted to AsciiDoc source blocks, with the appropriate language specified.
-   **Tables:** Markdown tables will be converted to AsciiDoc table syntax.
-   **Links:** Markdown links will be converted to AsciiDoc link syntax.
-   **Images:** Markdown image syntax will be converted to AsciiDoc image blocks.

### 1.4. Antora Structure

The `asciidocs/` directory will be structured as an Antora project with the following components:

-   **ucc111**: Linux Fundamentals
-   **ucc121**: Linux Expert
-   **ucc141**: Virtualization Fundamentals

Each component will have a single module (`ROOT`) and its own `nav.adoc` file to define the navigation structure.

## 2. Deployment Plan

A GitHub Actions workflow will be created to build and deploy the Antora site to GitHub Pages.

### 2.1. Workflow Triggers

The workflow will be triggered on pushes to the `main` branch.

### 2.2. Workflow Steps

1.  **Checkout Code:** The workflow will check out the repository content.
2.  **Set up Node.js:** It will set up a Node.js environment.
3.  **Install Antora:** It will install Antora and the site generator.
4.  **Build Antora Site:** The workflow will run the `antora` command to build the site.
5.  **Deploy to GitHub Pages:** The generated site will be deployed to the `gh-pages` branch.

### 2.3. GitHub Actions Workflow File

The following workflow file will be created at `.github/workflows/antora.yml`:

```yaml
name: Deploy Antora Site

on:
  push:
    branches:
      - main

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Set up Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '18'

      - name: Install Antora
        run: npm install -g @antora/cli @antora/site-generator-default

      - name: Build Antora site
        run: antora antora.yml

      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./build/site
```
