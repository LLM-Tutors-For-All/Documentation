# Bot integration documentation

This project uses [MkDocs](https://www.mkdocs.org/) with the
[Material for MkDocs](https://squidfunk.github.io/mkdocs-material/) theme.

## Run locally

Python 3 must be installed and available from PowerShell.

1. Create a virtual environment:

   ```powershell
   py -m venv .venv
   ```

2. Activate it:

   ```powershell
   .\.venv\Scripts\Activate.ps1
   ```

3. Install the dependencies:

   ```powershell
   py -m pip install -r requirements.txt
   ```

4. Start the development server:

   ```powershell
   mkdocs serve
   ```

5. Open <http://127.0.0.1:8000> in a browser.

MkDocs automatically reloads the site when files under `docs/` or
`mkdocs.yml` change.

## Build the website

Generate the static website in the `site/` directory:

```powershell
mkdocs build --strict
```

The generated `site/` directory can be deployed to any static web host.

## Publish with GitHub Pages

The workflow in `.github/workflows/deploy-docs.yml` builds and deploys the
website whenever changes are pushed to `main`. It can also be started manually
from the repository's **Actions** tab.

Before the first deployment, open the repository on GitHub and go to
**Settings > Pages**. Under **Build and deployment**, set **Source** to
**GitHub Actions**. Push this project to `main`, then follow the deployment in
the **Actions** tab.

## Documentation structure

```text
docs/
├── index.md
├── discord.md
└── slack.md
mkdocs.yml
requirements.txt
```