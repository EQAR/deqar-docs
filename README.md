# deqar-docs
MkDocs documentation of DEQAR

## Preview

- Available at: <https://docs.deqar.eu/>
- Edit files (in `master` branch)
- When committed, webhook triggers update of the website

## Installation (local)

1. Instal mkdocs to your computer: http://www.mkdocs.org/#installation
2. Clone repo
3. `cd ./deqar-docs`
4. `mkdocs serve`
5. Visit http://127.0.0.1:8000/ in your browser.
6. Edit/create pages in Markdown.
7. Don't forget to add pages to `mkdocs.yml`.
8. This will help: http://www.mkdocs.org/user-guide/writing-your-docs/

## Installation (Docker)

1. Clone <https://github.com/ctueck/mkdocs-docker>
1. Create `.env` with  `GITHUB_SOURCE=https://github.com/EQAR/deqar-docs.git`
1. Run `docker-compose build`
1. Run `docker-compose up -d`
1. Visit <http://localhost:8080>
