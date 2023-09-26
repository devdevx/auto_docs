# MkDocs

## Documentation

[Official doc](https://www.mkdocs.org).
[Publish](https://squidfunk.github.io/mkdocs-material/publishing-your-site/)

## Commands

- `mkdocs new [dir-name]` - Create a new project.
- `mkdocs serve` - Start the live-reloading docs server.
- `mkdocs build` - Build the documentation site.
- `mkdocs -h` - Print help message and exit.

## Project layout

````
    mkdocs.yml    # The configuration file.
    docs/
        index.md  # The documentation homepage.
        ...       # Other markdown pages, images and other files.
````

## Docker commands

Init project
````
docker run --rm -it -v "%cd%":/docs squidfunk/mkdocs-material new .
````
Live reload
````
docker run --rm -it -p 8000:8000 -v "%cd%":/docs squidfunk/mkdocs-material
````

## Publish in github

Github only allows pages in public repos for free tier
When deploying from branch use `gh-pages` branch
