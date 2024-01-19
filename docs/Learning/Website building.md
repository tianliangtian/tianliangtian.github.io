# How to build personal website using MkDocs
## MkDocs
MkDocs is a **fast**, **simple** and **downright gorgeous** static site generator that's geared towards building project documentation. Documentation source files are written in Markdown, and configured with a single YAML configuration file. You can easily customize your webpages, preview your site and host it in almost anywhere.
Run the following command to install mkdocs
```
pip install mkdocs
```
Run the following code to initialize the project
```
mkdocs new my-project
```
This will create a new folder in your current directory with basic files to build the site. `mkdocs.yml` is a configuration file, storing site configuration. `docs` is a folder which contains your documentation source files. You can also try the following command to generate these files directly in your current directory.
```
mkdocs new .
```
`mkdocs.yml` specifies basic site configurations. A simple demo is showing below.
```yml
site_name: tianliangtian's personal website
site_url: https://tianliangtian.github.io
site_author: tianliangtian

theme:
  name: material

nav:
  - Home: index.md
  - Learning: 
    - Git: Learning/Git.md
```
`site_name` is the name of the site. `site_url` is the place where you deploy your site.
You can customize your site in the `theme` block
`nav` block helps you to arrange the order, title, and nesting of each page in the navigation header. Remember to relate your source files in `docs` to those pages.
You can use the following command to preview your site in the given url.
```
mkdocs serve
```
The following commands generate static site files.
```
mkdocs build
```
## Material for MkDocs
## Github Pages
## Critical Steps
## Warning
## Referance
* https://www.mkdocs.org/