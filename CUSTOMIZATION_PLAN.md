# Antora UI Customization Plan

This document outlines the plan for customizing the Antora site's colors and fonts using a supplemental UI build.

## 1. Directory Structure

A `supplemental-ui` directory will be created at the root of the project. This directory will contain the custom styles for the site. The proposed structure is as follows:

```
supplemental-ui/
└── modules/
    └── ROOT/
        └── assets/
            └── css/
                └── custom.css
```

This structure mirrors the Antora UI bundle, making it easy to override the default styles.

## 2. Custom CSS File

The custom styles will be placed in a new file named `custom.css`. This file will be located at `supplemental-ui/modules/ROOT/assets/css/custom.css`.

This file will contain all the CSS rules needed to change the site's colors and fonts. For example:

```css
/* supplemental-ui/modules/ROOT/assets/css/custom.css */
:root {
  --primary-color: #007bff;
  --text-color: #333;
  --font-family-body: "Helvetica Neue", Helvetica, Arial, sans-serif;
}
```

## 3. `antora.yml` Changes

To apply the supplemental UI, the `antora.yml` file needs to be updated to reference the new directory. This is done by adding the `supplemental_files` key to the `ui` section.

The `ui` section of the `antora.yml` file should be modified as follows:

```yaml
ui:
  bundle:
    url: https://gitlab.com/antora/antora-ui-default/-/jobs/artifacts/master/raw/build/ui-bundle.zip?job=bundle-stable
    snapshot: true
  supplemental_files: ./supplemental-ui
```

This configuration tells Antora to look for supplemental UI files in the `supplemental-ui` directory and layer them on top of the default UI.

## 4. Implementation

The implementation of these changes will be handled by the `code` mode. The steps are:

1.  Create the `supplemental-ui` directory structure.
2.  Create the `custom.css` file with the desired styles.
3.  Update the `antora.yml` file to include the `supplemental_files` key.
