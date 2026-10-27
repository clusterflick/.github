# Clusterflick

**[Clusterflick](https://clusterflick.com)** is a free, open-source site listing
every film showing in London, from 450+ venues in one search: chains,
independents, film clubs, festivals and pop-ups. Each film shows its screenings
across every venue, with ratings from IMDb, Letterboxd, Rotten Tomatoes and
Metacritic, and filters for subtitled, audio-described, relaxed and
baby-friendly showings.

🎬 Looking for something to watch? Head to **https://clusterflick.com** 🍿

This organisation holds the code behind it. Listings are pulled from each
venue's own website several times a day, put into one format, matched to The
Movie Database, and built into a static site. The pipeline runs in the open as a
chain of GitHub Actions, one repository per stage (see [Pipeline](#pipeline)).

[![Venue health](<https://img.shields.io/endpoint?url=https://gist.githubusercontent.com/alistairjcbrown/8d80a800fce80abc822d054b9e91ba0c/raw/venue-health.json&logo=github&logoColor=rgba(255%2C255%2C255%2C0.5)&labelColor=343b43>)](https://github.com/clusterflick/data-analysed/actions/workflows/venue-health.yml)
[![LLM usage](<https://img.shields.io/endpoint?url=https://gist.githubusercontent.com/alistairjcbrown/8d80a800fce80abc822d054b9e91ba0c/raw/llm-usage.json&logo=github&logoColor=rgba(255%2C255%2C255%2C0.5)&labelColor=343b43>)](https://github.com/clusterflick/data-analysed/actions/workflows/llm-usage-log.yml)

## Using the Data

📄 For data you can use, see
**[clusterflick.com/data-licence](https://clusterflick.com/data-licence)**.

Most of the repositories below are internal build artifacts, published because
the pipeline runs in the open rather than offered for reuse. Each one carries a
`LICENSE-DATA` file saying which it is.

The code in every repository is separately available under the MIT licence.

## Repositories

**The site**

- [clusterflick.com](https://github.com/clusterflick/clusterflick.com) — the
  website
- [api-tmdb-search](https://github.com/clusterflick/api-tmdb-search) — the
  Cloudflare Worker behind the site's film search
- [branding](https://github.com/clusterflick/branding) — brand guide, logos and
  icons

**The data pipeline**

- [scripts](https://github.com/clusterflick/scripts) — the code behind every
  stage, with a module for each venue and ticketing source
- [data-retrieved](https://github.com/clusterflick/data-retrieved) — pulls raw
  listings from venue websites and ticketing platforms
- [data-transformed](https://github.com/clusterflick/data-transformed) — puts
  each venue's listings into one format and matches films to TMDB
- [data-diffed](https://github.com/clusterflick/data-diffed) — records what
  changed between runs
- [data-cached](https://github.com/clusterflick/data-cached) — caches TMDB
  metadata for every film
- [data-combined](https://github.com/clusterflick/data-combined) — merges every
  venue into the single dataset the site is built from
- [data-matched](https://github.com/clusterflick/data-matched) — adds ratings
  from IMDb, Letterboxd, Rotten Tomatoes and Metacritic
- [data-calendar](https://github.com/clusterflick/data-calendar) — calendar
  feeds, one per venue
- [host-non-web-sources](https://github.com/clusterflick/host-non-web-sources) —
  hand-transcribed listings for venues with nothing on the web to read

**Tooling and operations**

- [data-analysed](https://github.com/clusterflick/data-analysed) — finds new
  venues, checks listings against other sources, tracks pipeline reliability
- [manage.clusterflick.com](https://github.com/clusterflick/manage.clusterflick.com)
  — internal review site for the pipeline
- [analysis.clusterflick.com](https://github.com/clusterflick/analysis.clusterflick.com)
  — the original site, kept for reviewing the combined data
- [generate-spotlights](https://github.com/clusterflick/generate-spotlights) —
  social media posts
- [self-hosted-workflows](https://github.com/clusterflick/self-hosted-workflows)
  — workflows for the Raspberry Pi runners
- [themoviedb-data](https://github.com/clusterflick/themoviedb-data) — TMDB
  catalogue download for experimentation
- [release-downloader](https://github.com/clusterflick/release-downloader) —
  fork of a GitHub Action for downloading release assets
- [.github](https://github.com/clusterflick/.github) — this profile and shared
  reusable workflows

## Build Status

1. [![Data Retrieved status](https://github.com/clusterflick/data-retrieved/actions/workflows/retrieve.yml/badge.svg)](https://github.com/clusterflick/data-retrieved/actions)
   [![Retrieve unassisted runs](<https://img.shields.io/endpoint?url=https://gist.githubusercontent.com/alistairjcbrown/8d80a800fce80abc822d054b9e91ba0c/raw/retrieve-unassisted.json&logo=github&logoColor=rgba(255%2C255%2C255%2C0.5)&labelColor=343b43>)](https://github.com/clusterflick/data-analysed/actions/workflows/workflow-run-stats.yml)
   [![Retrieve average duration](<https://img.shields.io/endpoint?url=https://gist.githubusercontent.com/alistairjcbrown/8d80a800fce80abc822d054b9e91ba0c/raw/retrieve-duration.json&logo=github&logoColor=rgba(255%2C255%2C255%2C0.5)&labelColor=343b43>)](https://github.com/clusterflick/data-analysed/actions/workflows/workflow-run-stats.yml)
2. [![Data Transformed status](https://github.com/clusterflick/data-transformed/actions/workflows/transform.yml/badge.svg)](https://github.com/clusterflick/data-transformed/actions)
   [![Transform unassisted runs](<https://img.shields.io/endpoint?url=https://gist.githubusercontent.com/alistairjcbrown/8d80a800fce80abc822d054b9e91ba0c/raw/transform-unassisted.json&logo=github&logoColor=rgba(255%2C255%2C255%2C0.5)&labelColor=343b43>)](https://github.com/clusterflick/data-analysed/actions/workflows/workflow-run-stats.yml)
   [![Transform average duration](<https://img.shields.io/endpoint?url=https://gist.githubusercontent.com/alistairjcbrown/8d80a800fce80abc822d054b9e91ba0c/raw/transform-duration.json&logo=github&logoColor=rgba(255%2C255%2C255%2C0.5)&labelColor=343b43>)](https://github.com/clusterflick/data-analysed/actions/workflows/workflow-run-stats.yml)
   - [![Data Diffed status](https://github.com/clusterflick/data-diffed/actions/workflows/diff.yml/badge.svg)](https://github.com/clusterflick/data-diffed/actions)
     [![Diff average duration](<https://img.shields.io/endpoint?url=https://gist.githubusercontent.com/alistairjcbrown/8d80a800fce80abc822d054b9e91ba0c/raw/diff-duration.json&logo=github&logoColor=rgba(255%2C255%2C255%2C0.5)&labelColor=343b43>)](https://github.com/clusterflick/data-analysed/actions/workflows/workflow-run-stats.yml)
     _(only releases when something changed)_
     - [![Data Cached status](https://github.com/clusterflick/data-cached/actions/workflows/cache.yml/badge.svg)](https://github.com/clusterflick/data-cached/actions)
       _(runs whether or not the diff released)_
   - _also triggers `scripts` PR and `data-analysed`_ analysis scripts
3. [![Data Combined status](https://github.com/clusterflick/data-combined/actions/workflows/combine.yml/badge.svg)](https://github.com/clusterflick/data-combined/actions)
   [![Combine average duration](<https://img.shields.io/endpoint?url=https://gist.githubusercontent.com/alistairjcbrown/8d80a800fce80abc822d054b9e91ba0c/raw/combine-duration.json&logo=github&logoColor=rgba(255%2C255%2C255%2C0.5)&labelColor=343b43>)](https://github.com/clusterflick/data-analysed/actions/workflows/workflow-run-stats.yml)
   - [![Data Matched status](https://github.com/clusterflick/data-matched/actions/workflows/match.yml/badge.svg)](https://github.com/clusterflick/data-matched/actions)
     [![Match unassisted runs](<https://img.shields.io/endpoint?url=https://gist.githubusercontent.com/alistairjcbrown/8d80a800fce80abc822d054b9e91ba0c/raw/match-unassisted.json&logo=github&logoColor=rgba(255%2C255%2C255%2C0.5)&labelColor=343b43>)](https://github.com/clusterflick/data-analysed/actions/workflows/workflow-run-stats.yml)
     [![Match average duration](<https://img.shields.io/endpoint?url=https://gist.githubusercontent.com/alistairjcbrown/8d80a800fce80abc822d054b9e91ba0c/raw/match-duration.json&logo=github&logoColor=rgba(255%2C255%2C255%2C0.5)&labelColor=343b43>)](https://github.com/clusterflick/data-analysed/actions/workflows/workflow-run-stats.yml)
     - (only releases once per day)
   - [![Data Calendar status](https://github.com/clusterflick/data-calendar/actions/workflows/generate_calendar.yml/badge.svg)](https://github.com/clusterflick/data-calendar/actions)
     [![Calendar average duration](<https://img.shields.io/endpoint?url=https://gist.githubusercontent.com/alistairjcbrown/8d80a800fce80abc822d054b9e91ba0c/raw/calendar-duration.json&logo=github&logoColor=rgba(255%2C255%2C255%2C0.5)&labelColor=343b43>)](https://github.com/clusterflick/data-analysed/actions/workflows/workflow-run-stats.yml)
     - `clusterflick.com`
       [![Website status](https://github.com/clusterflick/clusterflick.com/actions/workflows/generate_site.yml/badge.svg)](https://github.com/clusterflick/clusterflick.com/actions)
       [![Website average duration](<https://img.shields.io/endpoint?url=https://gist.githubusercontent.com/alistairjcbrown/8d80a800fce80abc822d054b9e91ba0c/raw/website-duration.json&logo=github&logoColor=rgba(255%2C255%2C255%2C0.5)&labelColor=343b43>)](https://github.com/clusterflick/data-analysed/actions/workflows/workflow-run-stats.yml)
   - `analysis.clusterflick.com`
     [![Analysis site status](https://github.com/clusterflick/analysis.clusterflick.com/actions/workflows/generate_site.yml/badge.svg)](https://github.com/clusterflick/analysis.clusterflick.com/actions)
     [![Analysis site average duration](<https://img.shields.io/endpoint?url=https://gist.githubusercontent.com/alistairjcbrown/8d80a800fce80abc822d054b9e91ba0c/raw/analysis-site-duration.json&logo=github&logoColor=rgba(255%2C255%2C255%2C0.5)&labelColor=343b43>)](https://github.com/clusterflick/data-analysed/actions/workflows/workflow-run-stats.yml)

## Pipeline

```mermaid
flowchart LR
    retrieved["data-retrieved"]
    transformed["data-transformed"]
    calendar["data-calendar"]
    cached["data-cached"]
    diffed["data-diffed"]
    combined["data-combined"]
    matched["data-matched"]
    scripts["scripts"]
    analysed["data-analysed<br>(comparisons)"]
    runstats["data-analysed<br>(run stats)"]

    subgraph retrival[" "]
        direction TB
        retrieved --> retrival-release>Release]
    end

    subgraph transformation[" "]
        direction TB
        transformed --> transformation-release>Release]
    end

    subgraph calendars[" "]
        direction TB
        calendar --> calendar-release>Release]
    end

    subgraph caching[" "]
        direction TB
        cached --> cached-release>Release]
    end

    subgraph diffing[" "]
        direction TB
        diffed --"if changed"--> diffed-release>Release]
    end

    subgraph combination[" "]
        direction TB
        combined --> combined-release>Release]
    end

    subgraph matching[" "]
        direction TB
        matched --> matched-release>Release]
    end

    subgraph website[" "]
        direction TB
        clusterflick.com --> id1[[Generate website]]
        analysis["analysis.clusterflick.com"] --> id2[[Generate analysis site]]
    end

    retrival --triggers--> transformation
    transformation --triggers--> diffing
    transformation --triggers--> scripts
    transformation --triggers--> analysed
    transformation --triggers--> runstats
    diffing --triggers--> caching
    caching --triggers--> combination
    combination --triggers--> calendars
    combination --triggers--> matching
    combination --triggers--> analysis
    calendars --triggers--> clusterflick.com
    matching --"triggers (if new data)"--> clusterflick.com

```

## Tooling Status

### Development

- `scripts`
  [![Scripts CI](https://github.com/clusterflick/scripts/actions/workflows/ci.yml/badge.svg)](https://github.com/clusterflick/scripts/actions/workflows/ci.yml)
- `clusterflick.com`
  [![Website CI](https://github.com/clusterflick/clusterflick.com/actions/workflows/ci.yml/badge.svg)](https://github.com/clusterflick/clusterflick.com/actions/workflows/ci.yml)

### Social Media / Spotlights

- [![Generate Last Chance](https://github.com/clusterflick/generate-spotlights/actions/workflows/generate-last-chance.yml/badge.svg)](https://github.com/clusterflick/generate-spotlights/actions/workflows/generate-last-chance.yml)
- [![Generate New Films](https://github.com/clusterflick/generate-spotlights/actions/workflows/generate-new-films.yml/badge.svg)](https://github.com/clusterflick/generate-spotlights/actions/workflows/generate-new-films.yml)
- [![Generate Single Movie](https://github.com/clusterflick/generate-spotlights/actions/workflows/generate-single-movie.yml/badge.svg)](https://github.com/clusterflick/generate-spotlights/actions/workflows/generate-single-movie.yml)

### Data Maintenance

- [![Update TMDB Data](https://github.com/clusterflick/themoviedb-data/actions/workflows/update.yml/badge.svg)](https://github.com/clusterflick/themoviedb-data/actions/workflows/update.yml)
  _(daily at 11am UTC)_
- [![Check Venue Statuses](https://github.com/clusterflick/data-analysed/actions/workflows/check-statuses.yml/badge.svg)](https://github.com/clusterflick/data-analysed/actions/workflows/check-statuses.yml)
  _(manual)_
- [![Compare Releases](https://github.com/clusterflick/data-analysed/actions/workflows/compare-releases.yml/badge.svg)](https://github.com/clusterflick/data-analysed/actions/workflows/compare-releases.yml)
  _(after each transform)_
- [![Compare Accessible Screenings](<https://img.shields.io/endpoint?url=https://gist.githubusercontent.com/alistairjcbrown/8d80a800fce80abc822d054b9e91ba0c/raw/compare-accessible-screenings.json&logo=github&logoColor=rgba(255%2C255%2C255%2C0.5)&labelColor=343b43>)](https://github.com/clusterflick/data-analysed/actions/workflows/compare-accessible-screenings.yml)
  _(after each transform)_
- [![Compare CinemaGuide Screenings](<https://img.shields.io/endpoint?url=https://gist.githubusercontent.com/alistairjcbrown/8d80a800fce80abc822d054b9e91ba0c/raw/compare-cinemaguide-screenings.json&logo=github&logoColor=rgba(255%2C255%2C255%2C0.5)&labelColor=343b43>)](https://github.com/clusterflick/data-analysed/actions/workflows/compare-cinemaguide-screenings.yml)
  _(after each transform)_
- [![Update Test Titles](https://github.com/clusterflick/scripts/actions/workflows/update-test-titles.yml/badge.svg)](https://github.com/clusterflick/scripts/actions/workflows/update-test-titles.yml)
  _(after each transform)_
- [![Pipeline Run Stats](https://github.com/clusterflick/data-analysed/actions/workflows/workflow-run-stats.yml/badge.svg)](https://github.com/clusterflick/data-analysed/actions/workflows/workflow-run-stats.yml)
  _(after each transform — feeds the stability badges above)_

### Self-hosted Runner Maintenance

- [![Runner Stats](https://github.com/clusterflick/self-hosted-workflows/actions/workflows/runner-stats.yml/badge.svg)](https://github.com/clusterflick/self-hosted-workflows/actions/workflows/runner-stats.yml)
- [![Reset Dependencies](https://github.com/clusterflick/self-hosted-workflows/actions/workflows/free-space.yml/badge.svg)](https://github.com/clusterflick/self-hosted-workflows/actions/workflows/free-space.yml)
- [![Check SSD Health](https://github.com/clusterflick/self-hosted-workflows/actions/workflows/chcek-runner-storage.yml/badge.svg)](https://github.com/clusterflick/self-hosted-workflows/actions/workflows/chcek-runner-storage.yml)

## Security Audit (zizmor)

Each repo audits its GitHub Actions workflows with
[zizmor](https://docs.zizmor.sh) via the shared
[`.github`](https://github.com/clusterflick/.github/blob/main/.github/workflows/zizmor.yml)
reusable workflow.

### Pipeline

- data-retrieved
  [![data-retrieved zizmor](https://github.com/clusterflick/data-retrieved/actions/workflows/zizmor.yml/badge.svg)](https://github.com/clusterflick/data-retrieved/actions/workflows/zizmor.yml)
- data-transformed
  [![data-transformed zizmor](https://github.com/clusterflick/data-transformed/actions/workflows/zizmor.yml/badge.svg)](https://github.com/clusterflick/data-transformed/actions/workflows/zizmor.yml)
- data-calendar
  [![data-calendar zizmor](https://github.com/clusterflick/data-calendar/actions/workflows/zizmor.yml/badge.svg)](https://github.com/clusterflick/data-calendar/actions/workflows/zizmor.yml)
- data-cached
  [![data-cached zizmor](https://github.com/clusterflick/data-cached/actions/workflows/zizmor.yml/badge.svg)](https://github.com/clusterflick/data-cached/actions/workflows/zizmor.yml)
- data-diffed
  [![data-diffed zizmor](https://github.com/clusterflick/data-diffed/actions/workflows/zizmor.yml/badge.svg)](https://github.com/clusterflick/data-diffed/actions/workflows/zizmor.yml)
- data-combined
  [![data-combined zizmor](https://github.com/clusterflick/data-combined/actions/workflows/zizmor.yml/badge.svg)](https://github.com/clusterflick/data-combined/actions/workflows/zizmor.yml)
- data-matched
  [![data-matched zizmor](https://github.com/clusterflick/data-matched/actions/workflows/zizmor.yml/badge.svg)](https://github.com/clusterflick/data-matched/actions/workflows/zizmor.yml)
- data-analysed
  [![data-analysed zizmor](https://github.com/clusterflick/data-analysed/actions/workflows/zizmor.yml/badge.svg)](https://github.com/clusterflick/data-analysed/actions/workflows/zizmor.yml)

### Websites

- clusterflick.com
  [![clusterflick.com zizmor](https://github.com/clusterflick/clusterflick.com/actions/workflows/zizmor.yml/badge.svg)](https://github.com/clusterflick/clusterflick.com/actions/workflows/zizmor.yml)
- analysis.clusterflick.com
  [![analysis.clusterflick.com zizmor](https://github.com/clusterflick/analysis.clusterflick.com/actions/workflows/zizmor.yml/badge.svg)](https://github.com/clusterflick/analysis.clusterflick.com/actions/workflows/zizmor.yml)

### Tooling

- github
  [![.github zizmor](https://github.com/clusterflick/.github/actions/workflows/zizmor.yml/badge.svg)](https://github.com/clusterflick/.github/actions/workflows/zizmor.yml)
- scripts
  [![scripts zizmor](https://github.com/clusterflick/scripts/actions/workflows/zizmor.yml/badge.svg)](https://github.com/clusterflick/scripts/actions/workflows/zizmor.yml)
- generate-spotlights
  [![generate-spotlights zizmor](https://github.com/clusterflick/generate-spotlights/actions/workflows/zizmor.yml/badge.svg)](https://github.com/clusterflick/generate-spotlights/actions/workflows/zizmor.yml)
- self-hosted-workflows
  [![self-hosted-workflows zizmor](https://github.com/clusterflick/self-hosted-workflows/actions/workflows/zizmor.yml/badge.svg)](https://github.com/clusterflick/self-hosted-workflows/actions/workflows/zizmor.yml)
- release-downloader
  [![release-downloader zizmor](https://github.com/clusterflick/release-downloader/actions/workflows/zizmor.yml/badge.svg)](https://github.com/clusterflick/release-downloader/actions/workflows/zizmor.yml)
