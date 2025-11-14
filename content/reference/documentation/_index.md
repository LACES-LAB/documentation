---
title: Documentation
description: "Material on how to set up documentation for your project"
weight: 1
---

# Setting Up Documentation for SCOREC Projects

This guide walks you through creating documentation for your SCOREC project.

## Basic Steps

- Add comprehensive comments to your class, functions ...
- Choose your hosting platform based on project complexity
- Consider automating documentation builds in your CI/CD pipeline


## 1. Setting Up Doxygen

**Purpose:** [Doxygen](https://www.doxygen.nl/) automatically generates documentation from specially formatted code comments. This forms the foundation for most SCOREC software documentation. It is particularly useful for API documentation. See an example [here](https://scorec.github.io/core/index.html).

**Steps:**

1. **Install Doxygen**
   - Install doxygen ([instructions](https://www.doxygen.nl/manual/install.html)) or use an existing installation.

2. **Add Documentation Comments**
   - Use Doxygen comment syntax in your code. A simple example is like:
```cpp
     /**
       * \brief Brief description of the function
       * \param paramName Description of parameter
       * \return Description of return value
       */
```
   - Detailed syntax can be found in their [documentation](https://www.doxygen.nl/manual/docblocks.html)

3. **Create Configuration File**
   - Generate a default configuration file with `doxygen -g Doxyfile`. Alternatively, you can generate it from a template file called `doxyfile.in`. See [example here](https://github.com/SCOREC/core/blob/master/Doxyfile.in) from PUMI.
   - Customize settings (project name, input directories, output format).

4. **Generate Documentation**
   - Run: `doxygen Doxyfile`
   - Output will be in the specified directory (e.g. `html/` or `latex/`)

## 2. Enhancing with Sphinx (Optional)

While Doxygen handles API documentation well, [Sphinx](https://www.sphinx-doc.org/en/master/index.html) provides a more modern, extensible framework for comprehensive project documentation including tutorials, guides, and custom pages. Though Sphinx is primarily a Python tool, it can be integrated with Doxygen using [Breathe](https://breathe.readthedocs.io/en/latest/quickstart.html). Example documentation from redev can be found [here](https://scorec.github.io/redev/concepts/index.html)

**Steps:**

1. **Set Up Python Environment**
  - An example environment from redev is like:
```
Sphinx==8.2.3
sphinx-rtd-theme==3.0.2
sphinx-sitemap==2.6.0
breathe==4.35.0
```
  - Other sphinx add-ons can be added if needed.

2. **Initialize Sphinx**
  - Initialization helps you build the documentation structure quickly during initial setup. It is not needed after the initial configuration.
```bash
   sphinx-quickstart docs
```

3. **Configure Sphinx**
   - Edit `docs/conf.py` to include Breathe extension
   - Point Breathe to your Doxygen XML output
   - Customize theme and settings
   - Example can be found [here](https://github.com/Sichao25/redev/blob/main/docsDoxySphinx/conf.py).

4. **Create Content**
   - Write `.rst` files for guides, tutorials, and overview pages. Guide on `.rst` files can be found [here](https://www.sphinx-doc.org/en/master/usage/restructuredtext/basics.html).
   - Use Breathe directives to include Doxygen-generated API docs. An example from redev can be found [here](https://github.com/Sichao25/redev/blob/main/docsDoxySphinx/api/cpp_doxygen_sphinx.rst?plain=1).

5. **Build Documentation**
```bash
   # Generate Doxygen XML first
   doxygen Doxyfile
   
   # Build Sphinx documentation
   make html
```

## 3. Hosting Your Documentation

### GitHub Pages (Recommended for Quick Setup)

GitHub Pages offers free, straightforward hosting directly from your repository.

**Option A: Deploy via Branch**
- Create a `gh-pages` branch
- Push your generated HTML to this branch
- Enable GitHub Pages in repository settings (source: `gh-pages` branch)
- Documentation automatically updates on each push
- Consider using a cron job instead of manual push
- Example script available from [redev](https://github.com/Sichao25/redev/tree/main/docsDoxySphinx)

**Option B: Deploy via GitHub Actions**
- Create a workflow file (e.g. `.github/workflows/docs.yml`)
- Configure automated builds and deployments on push/merge
- Example workflow available in [PUMI](https://github.com/SCOREC/core/blob/master/.github/workflows/doxygen-gh-pages.yml)

### Read the Docs (For Advanced Needs)

**When to use:** [ReadtheDocs](https://docs.readthedocs.com/platform/stable/index.html) is ideal for projects requiring complex use case like automatic versioning or page analysis. An detailed comparison with GitHub Pages can be found [here](https://about.readthedocs.com/comparisons/github-pages/).

**Setup:**
1. Sign up at [readthedocs.org](https://readthedocs.org)
2. Connect your repository
3. Add a `.readthedocs.yaml` configuration file. Example can be found here.
4. Documentation builds automatically on commits
