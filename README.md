# SensorFun

The landing page for [sensorfun.net](https://sensorfun.net/). It lists the
SensorFun spaces and their projects. Each space is a separate repository
and site:

| Space | Site | Projects |
| ----- | ---- | -------- |
| ESP32 | `https://esp32.sensorfun.net/` | WebRTC — `https://esp32.sensorfun.net/#/projects/webrtc`<br>Flasher — `https://esp32.sensorfun.net/#/projects/flasher` |

## Site

`site/` is plain static HTML and CSS with no build step. Preview it with any
static file server, for example:

```sh
python3 -m http.server --directory site 8000
```

Then open `http://127.0.0.1:8000/`.

## Add a space or project

- New space: copy the ESP32 card in `site/index.html` and point its links at the
  space's own site. Each space site links back to `https://sensorfun.net/`.
- New project in an existing space: add an item to that card's project list,
  linking to the project's route on the space site.

## GitHub Pages

`.github/workflows/site-pages.yml` publishes `site/` on changes to `main`, or
when manually dispatched.

1. In **Settings → Pages**, choose **GitHub Actions** as source.
2. Set the custom domain to `sensorfun.net` and configure the apex DNS records
   GitHub Pages documents for custom domains.
3. Push to `main`, or run the workflow manually.

## Commit checks

Install [pre-commit](https://pre-commit.com/) 4 or newer and activate the hooks
once per clone:

```sh
python3 -m pip install 'pre-commit>=4,<5'
pre-commit install
pre-commit run --all-files
```

Commits check whitespace, YAML/JSON syntax, merge conflicts, large files,
private keys, and secrets with Gitleaks, using the same configuration as the
ESP32 repository. The first run downloads the hook environments. Gitleaks scans
staged changes when committing. To scan existing Git history, use
`gitleaks git --redact` separately with an installed Gitleaks binary.

Hooks must be installed in each clone and can be bypassed. Secret detection is
heuristic, so keep real credentials out of this repository.
