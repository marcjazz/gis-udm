# GIS-UDM Course Materials

This repository contains course plans, labs, and presentation materials for various courses at GIS-UDM.

## Documentation Site

All course content is organized and best viewed through our documentation site, which is automatically generated using [MkDocs](https://www.mkdocs.org/) with the [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/) theme.

The live site is deployed to GitHub Pages and can be accessed here: **[https://learn.kdmarc.xyz/](https://learn.kdmarc.xyz/)**

### Running Locally

To view the documentation site on your local machine:

1.  **Clone the repository:**

    ```bash
    git clone https://github.com/marcjazz/gis-udm.git
    cd gis-udm
    ```

2.  **Install dependencies:**

    ```bash
    pip install -r requirements.txt
    ```

3.  **Start the development server:**

    ```bash
    mkdocs serve
    ```

 The site will be available at `http://127.0.0.1:8000`.

## Presentations (Marp Slides)

The presentation slides in the `slides/` directory are created using [Marp](https://marp.app/). You can use the `marp-cli` tool to view, present, and export them.

### Setup

1.  **Install Node.js:** If you don't have it, install Node.js (which includes npm).

2.  **Install Marp CLI:**

    ```bash
    npm install -g @marp-team/marp-cli
    ```

### Viewing Slides Locally

To serve the slides with live-reloading:

```bash
marp --server slides/
```

This will start a server and you can navigate to the specific presentation file in your browser (e.g., `http://localhost:8080/linux_fundamentals/disk_design.md`).

### Exporting Slides

You can export the Markdown slides into HTML, PDF, or PPTX formats.

1.  **Export to HTML:**

    ```bash
    marp slides/linux_fundamentals/disk_design.md -o presentation.html
    ```

2.  **Export to PDF:**

    ```bash
    marp slides/linux_fundamentals/disk_design.md --pdf -o presentation.pdf
    ```

3.  **Export to PowerPoint:**

    ```bash
    marp slides/linux_fundamentals/disk_design.md --pptx -o presentation.pptx
    ```

