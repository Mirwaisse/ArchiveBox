<div align="center">
<img src="https://i.imgur.com/4nkFjdv.png" height="80px">
<h1>ArchiveBox<br/><sub>The open-source self-hosted web archive.</sub></h1>

▶️ <a href="https://github.com/pirate/ArchiveBox/wiki/Quickstart">Quickstart</a> |
<a href="https://archivebox.zervice.io/">Demo</a> |
<a href="https://github.com/pirate/ArchiveBox">Github</a> |
<a href="https://github.com/pirate/ArchiveBox/wiki">Documentation</a> |
<a href="#background--motivation">Info & Motivation</a> |
<a href="https://github.com/pirate/ArchiveBox/wiki/Web-Archiving-Community">Community</a> |
<a href="https://github.com/pirate/ArchiveBox/wiki/Roadmap">Roadmap</a>

<pre>
"Your own personal internet archive" (网站存档 / 爬虫)
</pre>

<!--<a href="http://webchat.freenode.net?channels=ArchiveBox&uio=d4"><img src="https://img.shields.io/badge/Community_chat-IRC-%2328A745.svg"/></a>-->

<a href="https://github.com/pirate/ArchiveBox/blob/master/LICENSE"><img src="https://img.shields.io/badge/Open_source-MIT-green.svg?logo=git&logoColor=green"/></a>
<a href="https://github.com/pirate/ArchiveBox/commits/dev"><img src="https://img.shields.io/github/last-commit/pirate/ArchiveBox.svg?logo=Sublime+Text&logoColor=green&label=Active"/></a>
<a href="https://github.com/pirate/ArchiveBox"><img src="https://img.shields.io/github/stars/pirate/ArchiveBox.svg?logo=github&label=Stars&logoColor=blue"/></a>
<a href="https://test.pypi.org/project/archivebox/"><img src="https://img.shields.io/badge/Python-%3E%3D3.7-yellow.svg?logo=python&logoColor=yellow"/></a>
<a href="https://github.com/pirate/ArchiveBox/wiki/Install#dependencies"><img src="https://img.shields.io/badge/Chromium-%3E%3D59-orange.svg?logo=Google+Chrome&logoColor=orange"/></a>
<a href="https://hub.docker.com/r/nikisweeting/archivebox"><img src="https://img.shields.io/badge/Docker-all%20platforms-lightblue.svg?logo=docker&logoColor=lightblue"/></a>

<hr/>
</div>

ArchiveBox is a powerful self-hosted internet archiving solution written in Python 3. You feed it URLs of pages you want to archive, and it saves them to disk in a varitety of formats depending on the configuration and the content it detects. ArchiveBox can be installed via [Docker](https://docs.docker.com/get-docker/) or [`pip3`](https://wiki.python.org/moin/BeginnersGuide/Download).

Once installed, URLs can be added via the command line `archivebox add` or the built-in Web UI `archivebox server`. It can ingest bookmarks from a service like Pocket/Pinboard, your entire browsing history, RSS feeds, or URLs one at a time.

The main index is a self-contained `data/index.sqlite3` file, and each snapshot is stored as a folder `data/archive/<timestamp>/`, with an easy-to-read `index.html` and `index.json` within. For each page, ArchiveBox auto-extracts many types of assets/media and saves them in standard formats, with out-of-the-box support for: 3 types of HTML snapshots (wget, Chrome headless, singlefile), a PDF snapshot, a screenshot, a WARC archive, git repositories, images, audio, video, subtitles, article text, and more. The snapshots are browseable and managable offline through the filesystem, the built-in webserver, or the Python API.


#### Quickstart

```bash
docker run -d -it -v ~/archivebox:/data -p 8000:8000 nikisweeting/archivebox server --init 0.0.0.0:8000
docker run -v ~/archivebox:/data -it nikisweeting/archivebox manage createsuperuser
docker run -v ~/archivebox:/data -it nikisweeting/archivebox add 'https://example.com'

open http://127.0.0.1:8000/admin/login/  # then click "Add" in the navbar
```

<div align="center">
<img src="https://i.imgur.com/lUuicew.png" width="400px">
<br/>

[DEMO: archivebox.zervice.io/](https://archivebox.zervice.io)  
For more information, see the [full Quickstart guide](https://github.com/pirate/ArchiveBox/wiki/Quickstart), [Usage](https://github.com/pirate/ArchiveBox/wiki/Usage), and [Configuration](https://github.com/pirate/ArchiveBox/wiki/Configuration) docs.
</div>

---


# Overview

ArchiveBox is a command line tool, self-hostable web-archiving server, and Python library all-in-one. It's available as a Python3 package or a Docker image, both methods provide the same CLI, Web UI, and on-disk data format.

It works on Docker, macOS, and Linux/BSD. Windows is not officially supported, but users have reported getting it working using the WSL2 + Docker.

To use ArchiveBox you start by creating a folder for your data to live in (it can be anywhere on your system), and running `archivebox init` inside of it. That will create a sqlite3 index and an `ArchiveBox.conf` file. After that, you can continue to add/remove/search/import/export/manage/config/etc using the CLI `archivebox help`, or you can run the Web UI (recommended):
```bash
archivebox manage createsuperuser
archivebox server 0.0.0.0:8000
open http://127.0.0.1:8000
```

The CLI is considered "stable", and the ArchiveBox Python API and REST APIs are in "beta".

At the end of the day, the goal is to sleep soundly knowing that the part of the internet you care about will be automatically preserved in multiple, durable long-term formats that will be accessible for decades (or longer). You can also self-host your archivebox server on a public domain to provide archive.org-style public access to your site snapshots.

<div align="center">
<img src="https://i.imgur.com/3tBL7PU.png" width="22%" alt="CLI Screenshot" align="top">
<img src="https://i.imgur.com/viklZNG.png" width="22%" alt="Desktop index screenshot" align="top">
<img src="https://i.imgur.com/RefWsXB.jpg" width="22%" alt="Desktop details page Screenshot"/>
<img src="https://i.imgur.com/M6HhzVx.png" width="22%" alt="Desktop details page Screenshot"/><br/>
<sup><a href="https://archive.sweeting.me/">Demo</a> | <a href="https://github.com/pirate/ArchiveBox/wiki/Usage">Usage</a> | <a href="#screenshots">Screenshots</a></sup>
<br/>
<sub>. . . . . . . . . . . . . . . . . . . . . . . . . . . .</sub>
</div><br/>


## Key Features

- [**Free & open source**](https://github.com/pirate/ArchiveBox/blob/master/LICENSE), doesn't require signing up for anything, stores all data locally
- [**Few dependencies**](https://github.com/pirate/ArchiveBox/wiki/Install#dependencies) and [simple command line interface](https://github.com/pirate/ArchiveBox/wiki/Usage#CLI-Usage)
- [**Comprehensive documentation**](https://github.com/pirate/ArchiveBox/wiki), [active development](https://github.com/pirate/ArchiveBox/wiki/Roadmap), and [rich community](https://github.com/pirate/ArchiveBox/wiki/Web-Archiving-Community)
- Easy to set up **[scheduled importing](https://github.com/pirate/ArchiveBox/wiki/Scheduled-Archiving) from multiple sources**
- Uses common, **durable, [long-term formats](#saves-lots-of-useful-stuff-for-each-imported-link)** like HTML, JSON, PDF, PNG, and WARC
- ~~**Suitable for paywalled / [authenticated content](https://github.com/pirate/ArchiveBox/wiki/Configuration#chrome_user_data_dir)** (can use your cookies)~~ (do not do this until v0.5 is released with some security fixes)
- **Doesn't require a constantly-running daemon**, proxy, or native app
- Provides a CLI, Python API, self-hosted web UI, and REST API (WIP)
- Architected to be able to run [**many varieties of scripts during archiving**](https://github.com/pirate/ArchiveBox/issues/51), e.g. to extract media, summarize articles, [scroll pages](https://github.com/pirate/ArchiveBox/issues/80), [close modals](https://github.com/pirate/ArchiveBox/issues/175), expand comment threads, etc.
- Can also [**mirror content to 3rd-party archiving services**](https://github.com/pirate/ArchiveBox/wiki/Configuration#submit_archive_dot_org) automatically for redundancy

## Input formats

ArchiveBox supports many input formats for URLs, including Pocket & Pinboard exports, Browser bookmarks, Browser history, plain text, HTML, markdown, and more!

```bash
echo 'http://example.com' | archivebox add
archivebox add 'https://example.com/some/page'
archivebox add < ~/Downloads/firefox_bookmarks_export.html
archivebox add < any_text_with_urls_in_it.txt
archivebox add --depth=1 'https://example.com/some/downloads.html'
archivebox add --depth=1 'https://news.ycombinator.com#2020-12-12'
```

- <img src="https://nicksweeting.com/images/bookmarks.png" height="22px"/> Browser history or bookmarks exports (Chrome, Firefox, Safari, IE, Opera, and more)
- <img src="https://nicksweeting.com/images/rss.svg" height="22px"/> RSS, XML, JSON, CSV, SQL, HTML, Markdown, TXT, or any other text-based format
- <img src="https://getpocket.com/favicon.ico" height="22px"/> Pocket, Pinboard, Instapaper, Shaarli, Delicious, Reddit Saved Posts, Wallabag, Unmark.it, OneTab, and more

See the [Usage: CLI](https://github.com/pirate/ArchiveBox/wiki/Usage#CLI-Usage) page for documentation and examples.

It also includes a built-in scheduled import feature and browser bookmarklet, so you can ingest URLs from RSS feeds, websites, or the filesystem regularly.

## Output formats

All of ArchiveBox's state (including the index, snapshot data, and config file) is stored in a single folder called the "ArchiveBox data folder". All `archivebox` CLI commands must be run from inside this folder, and you first create it by running `archivebox init`.

The on-disk layout is optimized to be easy to browse by hand and durable long-term. The main index is a standard sqlite3 database (it can also be exported as static JSON/HTML), and the archive snapshots are organized by date-added timestamp in the `archive/` subfolder. Each snapshot subfolder includes a static JSON and HTML index describing its contents, and the snapshot extractor outputs are plain files within the folder (e.g. `media/example.mp4`, `git/somerepo.git`, `static/someimage.png`, etc.)

```bash
 ls ./archive/<timestamp>/
```

- **Index:** `index.html` & `index.json` HTML and JSON index files containing metadata and details
- **Title:** `title` title of the site
- **Favicon:** `favicon.ico` favicon of the site
- **WGET Clone:** `example.com/page-name.html` wget clone of the site, with .html appended if not present
- **WARC:** `warc/<timestamp>.gz` gzipped WARC of all the resources fetched while archiving
- **PDF:** `output.pdf` Printed PDF of site using headless chrome
- **Screenshot:** `screenshot.png` 1440x900 screenshot of site using headless chrome
- **DOM Dump:** `output.html` DOM Dump of the HTML after rendering using headless chrome
- **URL to Archive.org:** `archive.org.txt` A link to the saved site on archive.org
- **Audio & Video:** `media/` all audio/video files + playlists, including subtitles & metadata with youtube-dl
- **Source Code:** `git/` clone of any repository found on github, bitbucket, or gitlab links
- _More coming soon! See the [Roadmap](https://github.com/pirate/ArchiveBox/wiki/Roadmap)..._

It does everything out-of-the-box by default, but you can disable or tweak [individual archive methods](https://github.com/pirate/ArchiveBox/wiki/Configuration) via environment variables or config file.

## Dependencies

You don't need to install all the dependencies, ArchiveBox will automatically enable the relevant modules based on whatever you have available, but it's recommended to use the official [Docker image](https://github.com/pirate/ArchiveBox/wiki/Docker) with everything preinstalled.

If you so choose, you can also install ArchiveBox and its dependencies directly on any Linux or macOS systems using the [automated setup script](https://github.com/pirate/ArchiveBox/wiki/Quickstart) or the [system package manager](https://github.com/pirate/ArchiveBox/wiki/Install).

ArchiveBox is written in Python 3 so it requires `python3` and `pip3` available on your system. It also uses a set of optional, but highly recommended external dependencies for archiving sites: `wget` (for plain HTML, static files, and WARC saving), `chromium` (for screenshots, PDFs, JS execution, and more), `youtube-dl` (for audio and video), `git` (for cloning git repos), and `nodejs` (for readability and singlefile), and more.

## Caveats

If you're importing URLs containing secret slugs or pages with private content (e.g Google Docs, CodiMD notepads, etc), you may want to disable some of the extractor modules to avoid leaking private URLs to 3rd party APIs during the archiving process.

Be aware that malicious archived JS can also read the contents of other pages in your archive due to snapshot CSRF and XSS protections being imperfect. See the [Security Overview](https://github.com/pirate/ArchiveBox/wiki/Security-Overview#stealth-mode) page for more details.

Support for saving multiple snapshots of each site over time will be [added soon](https://github.com/pirate/ArchiveBox/issues/179) (along with the ability to view diffs of the changes between runs). For now ArchiveBox is designed to only archive each URL with each extractor type once.

---

# Setup

## Docker

```bash
# Docker
mkdir data && cd data
docker run -v $PWD:/data -it nikisweeting/archivebox init
docker run -v $PWD:/data -it nikisweeting/archivebox add 'https://example.com'
docker run -v $PWD:/data -it nikisweeting/archivebox manage createsuperuser
docker run -v $PWD:/data -it -p 8000:8000 nikisweeting/archivebox server 0.0.0.0:8000

open http://127.0.0.1:8000
```

```bash
# Docker Compose
# first download: https://github.com/pirate/ArchiveBox/blob/master/docker-compose.yml
docker-compose run archivebox init
docker-compose run archivebox add 'https://example.com'
docker-compose run archivebox manage createsuperuser
docker-compose up
open http://127.0.0.1:8000
```

## Bare Metal
```bash
# Bare Metal
# Use apt on Ubuntu/Debian, brew on mac, or pkg on BSD
# You may need to add a ppa with a more recent version of nodejs
apt install python3 python3-pip python3-dev git curl wget youtube-dl chromium-browser

# Install Node + NPM
curl -s https://deb.nodesource.com/gpgkey/nodesource.gpg.key | apt-key add - \
  && echo 'deb https://deb.nodesource.com/node_14.x $(lsb_release -cs) main' >> /etc/apt/sources.list \
  && apt-get update \
  && apt-get install --no-install-recommends nodejs

# Make a directory to hold your collection
mkdir data && cd data    # (can be anywhere, doesn't have to be called data)

# Install python package (or do this in a .venv if you want)
pip install --upgrade archivebox

# Install node packages (needed for SingleFile, Readability, and Puppeteer)
npm install --prefix . 'git+https://github.com/pirate/ArchiveBox.git' 

archivebox init
archivebox add 'https://example.com'  # add URLs as args pipe them in via stdin

# it can injest links from many formats, including RSS/JSON/XML/MD/TXT and more
curl https://getpocket.com/users/USERNAME/feed/all | archivebox add
archivebox add --depth=1 https://example.com/table-of-contents.html
```

Once you've added your first links, open `data/index.html` in a browser to view the static archive.

You can also start it as a server with a full web UI to manage your links:

```bash
archivebox manage createsuperuser
archivebox server
```

You can visit `http://127.0.0.1:8000` in your browser to access it.


---

<div align="center">
<img src="https://i.imgur.com/PVO88AZ.png" width="80%"/>
</div>

---

# Background & Motivation

Vast treasure troves of knowledge are lost every day on the internet to link rot. As a society, we have an imperative to preserve some important parts of that treasure, just like we preserve our books, paintings, and music in physical libraries long after the originals go out of print or fade into obscurity.

Whether it's to resist censorship by saving articles before they get taken down or edited, or
just to save a collection of early 2010's flash games you love to play, having the tools to
archive internet content enables to you save the stuff you care most about before it disappears.

<div align="center">
<img src="https://i.imgur.com/bC6eZcV.png" width="50%"/><br/>
 <sup><i>Image from <a href="https://digiday.com/media/wtf-link-rot/">WTF is Link Rot?</a>...</i><br/></sup>
</div>

The balance between the permanence and ephemeral nature of content on the internet is part of what makes it beautiful.
I don't think everything should be preserved in an automated fashion, making all content permanent and never removable, but I do think people should be able to decide for themselves and effectively archive specific content that they care about.

Because modern websites are complicated and often rely on dynamic content,
ArchiveBox archives the sites in **several different formats** beyond what public archiving services like Archive.org and Archive.is are capable of saving. Using multiple methods and the market-dominant browser to execute JS ensures we can save even the most complex, finicky websites in at least a few high-quality, long-term data formats.

All the archived links are stored by date bookmarked in `./archive/<timestamp>`, and everything is indexed nicely with JSON & HTML files. The intent is for all the content to be viewable with common software in 50 - 100 years without needing to run ArchiveBox in a VM.

## Comparison to Other Projects

▶ **Check out our [community page](https://github.com/pirate/ArchiveBox/wiki/Web-Archiving-Community) for an index of web archiving initiatives and projects.**

<img src="https://i.imgur.com/4nkFjdv.png" width="10%" align="left"/> The aim of ArchiveBox is to go beyond what the Wayback Machine and other public archiving services can do, by adding a headless browser to replay sessions accurately, and by automatically extracting all the content in multiple redundant formats that will survive being passed down to historians and archivists through many generations.

#### User Interface & Intended Purpose

ArchiveBox differentiates itself from [similar projects](https://github.com/pirate/ArchiveBox/wiki/Web-Archiving-Community#Web-Archiving-Projects) by being a simple, one-shot CLI interface for users to ingest bulk feeds of URLs over extended periods, as opposed to being a backend service that ingests individual, manually-submitted URLs from a web UI. However, we also have the option to add urls via a web interface through our Django frontend.

#### Private Local Archives vs Centralized Public Archives

Unlike crawler software that starts from a seed URL and works outwards, or public tools like Archive.org designed for users to manually submit links from the public internet, ArchiveBox tries to be a set-and-forget archiver suitable for archiving your entire browsing history, RSS feeds, or bookmarks, ~~including private/authenticated content that you wouldn't otherwise share with a centralized service~~ (do not do this until v0.5 is released with some security fixes). Also by having each user store their own content locally, we can save much larger portions of everyone's browsing history than a shared centralized service would be able to handle.

#### Storage Requirements

Because ArchiveBox is designed to ingest a firehose of browser history and bookmark feeds to a local disk, it can be much more disk-space intensive than a centralized service like the Internet Archive or Archive.today. However, as storage space gets cheaper and compression improves, you should be able to use it continuously over the years without having to delete anything. In my experience, ArchiveBox uses about 5gb per 1000 articles, but your milage may vary depending on which options you have enabled and what types of sites you're archiving. By default, it archives everything in as many formats as possible, meaning it takes more space than a using a single method, but more content is accurately replayable over extended periods of time. Storage requirements can be reduced by using a compressed/deduplicated filesystem like ZFS/BTRFS, or by setting `SAVE_MEDIA=False` to skip audio & video files.

## Learn more

Whether you want to learn which organizations are the big players in the web archiving space, want to find a specific open-source tool for your web archiving need, or just want to see where archivists hang out online, our Community Wiki page serves as an index of the broader web archiving community. Check it out to learn about some of the coolest web archiving projects and communities on the web!

<img src="https://i.imgur.com/0ZOmOvN.png" width="14%" align="right"/>

- [Community Wiki](https://github.com/pirate/ArchiveBox/wiki/Web-Archiving-Community)
  - [The Master Lists](https://github.com/pirate/ArchiveBox/wiki/Web-Archiving-Community#The-Master-Lists)  
    _Community-maintained indexes of archiving tools and institutions._
  - [Web Archiving Software](https://github.com/pirate/ArchiveBox/wiki/Web-Archiving-Community#Web-Archiving-Projects)  
    _Open source tools and projects in the internet archiving space._
  - [Reading List](https://github.com/pirate/ArchiveBox/wiki/Web-Archiving-Community#Reading-List)  
    _Articles, posts, and blogs relevant to ArchiveBox and web archiving in general._
  - [Communities](https://github.com/pirate/ArchiveBox/wiki/Web-Archiving-Community#Communities)  
    _A collection of the most active internet archiving communities and initiatives._
- Check out the ArchiveBox [Roadmap](https://github.com/pirate/ArchiveBox/wiki/Roadmap) and [Changelog](https://github.com/pirate/ArchiveBox/wiki/Changelog)
- Learn why archiving the internet is important by reading the "[On the Importance of Web Archiving](https://parameters.ssrc.org/2018/09/on-the-importance-of-web-archiving/)" blog post.
- Or reach out to me for questions and comments via [@theSquashSH](https://twitter.com/thesquashSH) on Twitter.

---

# Documentation

<img src="https://read-the-docs-guidelines.readthedocs-hosted.com/_images/logo-dark.png" width="13%" align="right"/>

We use the [Github wiki system](https://github.com/pirate/ArchiveBox/wiki) and [Read the Docs](https://archivebox.readthedocs.io/en/latest/) (WIP) for documentation.

You can also access the docs locally by looking in the [`ArchiveBox/docs/`](https://github.com/pirate/ArchiveBox/wiki/Home) folder.

## Getting Started

- [Quickstart](https://github.com/pirate/ArchiveBox/wiki/Quickstart)
- [Install](https://github.com/pirate/ArchiveBox/wiki/Install)
- [Docker](https://github.com/pirate/ArchiveBox/wiki/Docker)

## Reference

- [Usage](https://github.com/pirate/ArchiveBox/wiki/Usage)
- [Configuration](https://github.com/pirate/ArchiveBox/wiki/Configuration)
- [Supported Sources](https://github.com/pirate/ArchiveBox/wiki/Quickstart#2-get-your-list-of-urls-to-archive)
- [Supported Outputs](https://github.com/pirate/ArchiveBox/wiki#can-save-these-things-for-each-site)
- [Scheduled Archiving](https://github.com/pirate/ArchiveBox/wiki/Scheduled-Archiving)
- [Publishing Your Archive](https://github.com/pirate/ArchiveBox/wiki/Publishing-Your-Archive)
- [Chromium Install](https://github.com/pirate/ArchiveBox/wiki/Install-Chromium)
- [Security Overview](https://github.com/pirate/ArchiveBox/wiki/Security-Overview)
- [Troubleshooting](https://github.com/pirate/ArchiveBox/wiki/Troubleshooting)
- [Python API](https://docs.archivebox.io/en/latest/modules.html)
- REST API (coming soon...)

## More Info

- [Tickets](https://github.com/pirate/ArchiveBox/issues)
- [Roadmap](https://github.com/pirate/ArchiveBox/wiki/Roadmap)
- [Changelog](https://github.com/pirate/ArchiveBox/wiki/Changelog)
- [Donations](https://github.com/pirate/ArchiveBox/wiki/Donations)
- [Background & Motivation](https://github.com/pirate/ArchiveBox#background--motivation)
- [Web Archiving Community](https://github.com/pirate/ArchiveBox/wiki/Web-Archiving-Community)

---

# ArchiveBox Development

All contributions to ArchiveBox are welcomed! Check our [issues](https://github.com/pirate/ArchiveBox/issues) and [Roadmap](https://github.com/pirate/ArchiveBox/wiki/Roadmap) for things to work on, and please open an issue to discuss your proposed implementation before working on things! Otherwise we may have to close your PR if it doesn't align with our roadmap.

### Setup the dev environment

```python3
git clone https://github.com/pirate/ArchiveBox
cd ArchiveBox
git checkout master  # or the branch you want to test
git pull

# Install ArchiveBox + python dependencies
python3 -m venv .venv && source .venv/bin/activate && pip install -e .[dev]
# or
pipenv install --dev && pipenv shell

# Install node dependencies
npm install

# Optional: install the extractor dependencies
./bin/setup.sh
```

### Common development tasks

See the `./bin/` folder and read the source of the bash scripts within.
You can also run all these in Docker. For more examples see the Github Actions CI/CD tests that are run: `.github/workflows/*.yaml`.

#### Run the linters

```bash
./bin/lint.sh
```
(uses `flake8` and `mypy`)

#### Run the integration tests

```bash
./bin/test.sh
```
(uses `pytest -s`)

#### Build the docs, pip package, and docker image

```bash
./bin/build.sh

# or individually:
./bin/build_docs.sh
./bin/build_pip.sh
./bin/build_docker.sh
```

#### Roll a release

```bash
./bin/release.sh
```
(bumps the version, builds, and pushes a release to PyPI, Docker Hub, and Github Packages)


---

<div align="center">
<br/><br/>
<img src="https://raw.githubusercontent.com/Monadical-SAS/redux-time/HEAD/examples/static/jeremy.jpg" height="40px"/>
<br/>
<sub><i>This project is maintained mostly in <a href="https://nicksweeting.com/blog#About">my spare time</a> with the help from generous contributors and Monadical.com.</i></sub>
<br/><br/>

<br/>
<a href="https://github.com/sponsors/pirate">Sponsor us on Github</a>
<br>
<br>
<a href="https://www.patreon.com/theSquashSH"><img src="https://img.shields.io/badge/Donate_to_support_development-via_Patreon-%23DD5D76.svg?style=flat"/></a>
<br/>

<a href="https://twitter.com/thesquashSH"><img src="https://img.shields.io/badge/Tweet-%40theSquashSH-blue.svg?style=flat"/></a>
<a href="https://github.com/pirate/ArchiveBox"><img src="https://img.shields.io/github/stars/pirate/ArchiveBox.svg?style=flat&label=Star+on+Github"/></a>

<br/><br/>

</div>
