# Clusterflick

This is the Github org for the code that powers ClusterFlick 🍿

🎬 Looking to see what movies are showing? View them at https://clusterflick.com

## Build Status

1. [![Data Retrieved status](https://github.com/clusterflick/data-retrieved/actions/workflows/retrieve.yml/badge.svg)](https://github.com/clusterflick/data-retrieved/actions)
2. [![Data Transformed status](https://github.com/clusterflick/data-transformed/actions/workflows/transform.yml/badge.svg)](https://github.com/clusterflick/data-transformed/actions)
   - [![Data Calendar status](https://github.com/clusterflick/data-calendar/actions/workflows/generate_calendar.yml/badge.svg)](https://github.com/clusterflick/data-calendar/actions)
   - [![Data Cached status](https://github.com/clusterflick/data-cached/actions/workflows/cache.yml/badge.svg)](https://github.com/clusterflick/data-cached/actions)
3. [![Data Combined status](https://github.com/clusterflick/data-combined/actions/workflows/combine.yml/badge.svg)](https://github.com/clusterflick/data-combined/actions)
   - [![Data Matched status](https://github.com/clusterflick/data-matched/actions/workflows/match.yml/badge.svg)](https://github.com/clusterflick/data-matched/actions) _(triggers website if not skipped)_
   - `clusterflick.com` [![Website status](https://github.com/clusterflick/clusterflick.com/actions/workflows/generate_site.yml/badge.svg)](https://github.com/clusterflick/clusterflick.com/actions)
   - `analysis.clusterflick.com` [![Analysis site status](https://github.com/clusterflick/analysis.clusterflick.com/actions/workflows/generate_site.yml/badge.svg)](https://github.com/clusterflick/analysis.clusterflick.com/actions)

## Pipeline

```mermaid
flowchart LR
    retrieved["data-retrieved"]
    transformed["data-transformed"]
    calendar["data-calendar"]
    cached["data-cached"]
    combined["data-combined"]
    matched["data-matched"]

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
    caching --triggers--> combination
    combination --triggers--> matching
    combination --triggers--> website
    matching --"triggers (if new data)"--> website
    combination --triggers--> analysis

```

## Tooling Status

### Development

- `scripts` [![Scripts CI](https://github.com/clusterflick/scripts/actions/workflows/ci.yml/badge.svg)](https://github.com/clusterflick/scripts/actions/workflows/ci.yml)
- `clusterflick.com` [![Website CI](https://github.com/clusterflick/clusterflick.com/actions/workflows/ci.yml/badge.svg)](https://github.com/clusterflick/clusterflick.com/actions/workflows/ci.yml)

### Social Media / Spotlights

- [![Generate Last Chance](https://github.com/clusterflick/generate-spotlights/actions/workflows/generate-last-chance.yml/badge.svg)](https://github.com/clusterflick/generate-spotlights/actions/workflows/generate-last-chance.yml)
- [![Generate New Films](https://github.com/clusterflick/generate-spotlights/actions/workflows/generate-new-films.yml/badge.svg)](https://github.com/clusterflick/generate-spotlights/actions/workflows/generate-new-films.yml)
- [![Generate Single Movie](https://github.com/clusterflick/generate-spotlights/actions/workflows/generate-single-movie.yml/badge.svg)](https://github.com/clusterflick/generate-spotlights/actions/workflows/generate-single-movie.yml)

### Data Maintenance

- [![Update TMDB Data](https://github.com/clusterflick/themoviedb-data/actions/workflows/update.yml/badge.svg)](https://github.com/clusterflick/themoviedb-data/actions/workflows/update.yml)
- [![Check Venue Statuses](https://github.com/clusterflick/data-analysed/actions/workflows/check-statuses.yml/badge.svg)](https://github.com/clusterflick/data-analysed/actions/workflows/check-statuses.yml)
- [![Compare Releases](https://github.com/clusterflick/data-analysed/actions/workflows/compare-releases.yml/badge.svg)](https://github.com/clusterflick/data-analysed/actions/workflows/compare-releases.yml)
- [![Update Test Titles](https://github.com/clusterflick/scripts/actions/workflows/update-test-titles.yml/badge.svg)](https://github.com/clusterflick/scripts/actions/workflows/update-test-titles.yml)

### Self-hosted Runner Maintenance

- [![Runner Stats](https://github.com/clusterflick/self-hosted-workflows/actions/workflows/runner-stats.yml/badge.svg)](https://github.com/clusterflick/self-hosted-workflows/actions/workflows/runner-stats.yml)
- [![Reset Dependencies](https://github.com/clusterflick/self-hosted-workflows/actions/workflows/free-space.yml/badge.svg)](https://github.com/clusterflick/self-hosted-workflows/actions/workflows/free-space.yml)
- [![Check SD Card Health](https://github.com/clusterflick/self-hosted-workflows/actions/workflows/check-sd-card.yml/badge.svg)](https://github.com/clusterflick/self-hosted-workflows/actions/workflows/check-sd-card.yml)
