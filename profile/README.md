# Clusterflick

This is the Github org for the code that powers ClusterFlick 🍿

🎬 Looking to see what movies are showing? View them at https://clusterflick.com

## Build Status

1. [![Data Retrieved status](https://github.com/clusterflick/data-retrieved/actions/workflows/retrieve.yml/badge.svg)](https://github.com/clusterflick/data-retrieved/actions)
2. [![Data Transformed status](https://github.com/clusterflick/data-transformed/actions/workflows/transform.yml/badge.svg)](https://github.com/clusterflick/data-transformed/actions)
   - [![Data Calendar status](https://github.com/clusterflick/data-calendar/actions/workflows/generate_calendar.yml/badge.svg)](https://github.com/clusterflick/data-calendar/actions)
   - [![Data Cached status](https://github.com/clusterflick/data-cached/actions/workflows/cache.yml/badge.svg)](https://github.com/clusterflick/data-cached/actions)
3. [![Data Combined status](https://github.com/clusterflick/data-combined/actions/workflows/combine.yml/badge.svg)](https://github.com/clusterflick/data-combined/actions)
   - [![Data Matched status](https://github.com/clusterflick/data-matched/actions/workflows/match.yml/badge.svg)](https://github.com/clusterflick/data-matched/actions) *(triggers website only if new data)*
   - [![Website status](https://github.com/clusterflick/clusterflick.com/actions/workflows/generate_site.yml/badge.svg)](https://github.com/clusterflick/clusterflick.com/actions)

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
    end

    retrival --triggers--> transformation
    transformation --triggers--> calendars
    transformation --triggers--> caching
    caching --triggers--> combination
    combination --triggers--> matching
    combination --triggers--> website
    matching --"triggers (if new data)"--> website

```
