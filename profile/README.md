# Clusterflick

This is the Github org for the code that powers ClusterFlick 🍿

🎬 Looking to see what movies are showing? View them at https://clusterflick.com

## Build Status

1. [![Data Retrieved status](https://github.com/clusterflick/data-retrieved/actions/workflows/retrieve.yml/badge.svg)](https://github.com/clusterflick/data-retrieved/actions)
2. [![Data Transformed status](https://github.com/clusterflick/data-transformed/actions/workflows/transform.yml/badge.svg)](https://github.com/clusterflick/data-transformed/actions)
   - [![Data Calendar status](https://github.com/clusterflick/data-calendar/actions/workflows/generate_calendar.yml/badge.svg)](https://github.com/clusterflick/data-calendar/actions)
   - [![Data Cached status](https://github.com/clusterflick/data-cached/actions/workflows/cache.yml/badge.svg)](https://github.com/clusterflick/data-cached/actions)
   - _also triggers `scripts` and `data-analysed`_
3. [![Data Combined status](https://github.com/clusterflick/data-combined/actions/workflows/combine.yml/badge.svg)](https://github.com/clusterflick/data-combined/actions)
   - [![Data Matched status](https://github.com/clusterflick/data-matched/actions/workflows/match.yml/badge.svg)](https://github.com/clusterflick/data-matched/actions)
     _(triggers website if not skipped)_
   - `clusterflick.com`
     [![Website status](https://github.com/clusterflick/clusterflick.com/actions/workflows/generate_site.yml/badge.svg)](https://github.com/clusterflick/clusterflick.com/actions)
   - `analysis.clusterflick.com`
     [![Analysis site status](https://github.com/clusterflick/analysis.clusterflick.com/actions/workflows/generate_site.yml/badge.svg)](https://github.com/clusterflick/analysis.clusterflick.com/actions)

## Pipeline

```mermaid
flowchart LR
    retrieved["data-retrieved"]
    transformed["data-transformed"]
    calendar["data-calendar"]
    cached["data-cached"]
    combined["data-combined"]
    matched["data-matched"]
    scripts["scripts"]
    analysed["data-analysed"]

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
    transformation --triggers--> calendars
    transformation --triggers--> caching
    transformation --triggers--> scripts
    transformation --triggers--> analysed
    caching --triggers--> combination
    combination --triggers--> matching
    combination --triggers--> website
    matching --"triggers (if new data)"--> website
    combination --triggers--> analysis

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
- [![Compare Accessible Screenings](https://github.com/clusterflick/data-analysed/actions/workflows/compare-accessible-screenings.yml/badge.svg)](https://github.com/clusterflick/data-analysed/actions/workflows/compare-accessible-screenings.yml)
  _(after each transform)_
- [![Compare CinemaGuide Screenings](https://github.com/clusterflick/data-analysed/actions/workflows/compare-cinemaguide-screenings.yml/badge.svg)](https://github.com/clusterflick/data-analysed/actions/workflows/compare-cinemaguide-screenings.yml)
  _(after each transform)_
- [![Update Test Titles](https://github.com/clusterflick/scripts/actions/workflows/update-test-titles.yml/badge.svg)](https://github.com/clusterflick/scripts/actions/workflows/update-test-titles.yml)
  _(after each transform)_

### Self-hosted Runner Maintenance

- [![Runner Stats](https://github.com/clusterflick/self-hosted-workflows/actions/workflows/runner-stats.yml/badge.svg)](https://github.com/clusterflick/self-hosted-workflows/actions/workflows/runner-stats.yml)
- [![Reset Dependencies](https://github.com/clusterflick/self-hosted-workflows/actions/workflows/free-space.yml/badge.svg)](https://github.com/clusterflick/self-hosted-workflows/actions/workflows/free-space.yml)
- [![Check SSD Health](https://github.com/clusterflick/self-hosted-workflows/actions/workflows/chcek-runner-storage.yml/badge.svg)](https://github.com/clusterflick/self-hosted-workflows/actions/workflows/chcek-runner-storage.yml)

## Security Audit (zizmor)

Each repo audits its GitHub Actions workflows with [zizmor](https://docs.zizmor.sh) via the shared [`.github`](https://github.com/clusterflick/.github/blob/main/.github/workflows/zizmor.yml) reusable workflow.

### Pipeline

- [![data-retrieved zizmor](https://github.com/clusterflick/data-retrieved/actions/workflows/zizmor.yml/badge.svg)](https://github.com/clusterflick/data-retrieved/actions/workflows/zizmor.yml)
- [![data-transformed zizmor](https://github.com/clusterflick/data-transformed/actions/workflows/zizmor.yml/badge.svg)](https://github.com/clusterflick/data-transformed/actions/workflows/zizmor.yml)
- [![data-calendar zizmor](https://github.com/clusterflick/data-calendar/actions/workflows/zizmor.yml/badge.svg)](https://github.com/clusterflick/data-calendar/actions/workflows/zizmor.yml)
- [![data-cached zizmor](https://github.com/clusterflick/data-cached/actions/workflows/zizmor.yml/badge.svg)](https://github.com/clusterflick/data-cached/actions/workflows/zizmor.yml)
- [![data-combined zizmor](https://github.com/clusterflick/data-combined/actions/workflows/zizmor.yml/badge.svg)](https://github.com/clusterflick/data-combined/actions/workflows/zizmor.yml)
- [![data-matched zizmor](https://github.com/clusterflick/data-matched/actions/workflows/zizmor.yml/badge.svg)](https://github.com/clusterflick/data-matched/actions/workflows/zizmor.yml)
- [![data-analysed zizmor](https://github.com/clusterflick/data-analysed/actions/workflows/zizmor.yml/badge.svg)](https://github.com/clusterflick/data-analysed/actions/workflows/zizmor.yml)

### Websites

- [![clusterflick.com zizmor](https://github.com/clusterflick/clusterflick.com/actions/workflows/zizmor.yml/badge.svg)](https://github.com/clusterflick/clusterflick.com/actions/workflows/zizmor.yml)
- [![analysis.clusterflick.com zizmor](https://github.com/clusterflick/analysis.clusterflick.com/actions/workflows/zizmor.yml/badge.svg)](https://github.com/clusterflick/analysis.clusterflick.com/actions/workflows/zizmor.yml)

### Tooling

- [![.github zizmor](https://github.com/clusterflick/.github/actions/workflows/zizmor.yml/badge.svg)](https://github.com/clusterflick/.github/actions/workflows/zizmor.yml)
- [![scripts zizmor](https://github.com/clusterflick/scripts/actions/workflows/zizmor.yml/badge.svg)](https://github.com/clusterflick/scripts/actions/workflows/zizmor.yml)
- [![generate-spotlights zizmor](https://github.com/clusterflick/generate-spotlights/actions/workflows/zizmor.yml/badge.svg)](https://github.com/clusterflick/generate-spotlights/actions/workflows/zizmor.yml)
- [![self-hosted-workflows zizmor](https://github.com/clusterflick/self-hosted-workflows/actions/workflows/zizmor.yml/badge.svg)](https://github.com/clusterflick/self-hosted-workflows/actions/workflows/zizmor.yml)
- [![release-downloader zizmor](https://github.com/clusterflick/release-downloader/actions/workflows/zizmor.yml/badge.svg)](https://github.com/clusterflick/release-downloader/actions/workflows/zizmor.yml)
