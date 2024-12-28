# deqar-docs
MkDocs documentation of DEQAR

## Installation (local)

1. Clone repo: `git clone git@github.com:EQAR/deqar-docs.git`
1. `cd ./deqar-docs`
1. Create Python environment (`virtualenv env`, `. env/bin/activate`)
1. Install MkDocs: `pip install -r requirements.txt`
1. `mkdocs serve`
1. Visit http://127.0.0.1:8000/ in your browser.
1. Edit/create pages in Markdown.
1. Don't forget to add pages to `mkdocs.yml`.
1. Commit changes.
1. This will help: http://www.mkdocs.org/user-guide/writing-your-docs/

## Deploy (GitHub pages)

1. Build version: `mike deploy [version]`
1. Push all branches (incl. `gh-pages`): `git push --all`

