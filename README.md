# Space/Time Directory - Installation

- Create directory `spacetime`, somewhere on your file system
- In this directory, create four directories:
  - `tools`
  - `services`
  - `etl-modules`
  - `data`
- And, create an empty file `config.yml`

Alternatively, you could also use Space/Time's [Ansible playbooks](https://github.com/nypl-spacetime/ansible-playbooks), and run them locally.

## Prerequisites

- Node.js

## Install databases
- Install databases:
  - [Elasticsearch](https://www.elastic.co/downloads/elasticsearch)
  - [Neo4j](http://neo4j.com/download) or `brew install neo4j`
  - [PostgreSQL](http://www.postgresql.org/download/) with [PostGIS](http://postgis.net/install/). Enable PostGIS in your database by running this query: `CREATE EXTENSION postgis;`

TODO: create PG database `spacetime`

By default, Space/Time uses the default ports, users and passwords for all databases. To override this, edit your configuration file.

## Configuration

For Space/Time to run, `config.yml` needs to hold a minimum of configuration options:

```yml
api:
  dataDir: /path/to/spacetime/data/api
  admin:
    name: spacetime
    password: password

etl:
  moduleDir: /path/to/spacetime/etl-modules
  modulePrefix: etl-
  outputDir: /path/to/spacetime/data/etl
  modules:
    geonames:
      extraUris:
      filters:
        - countryCode: US
          admin1Code: NY
        - countryCode: US
          admin1Code: NJ
      relations:
        liesIn: hg:liesIn
      types:
        PCLI: hg:Country
        PPLA2: hg:Borough
        ADM1: hg:State
        ADM2: hg:County
        PPLX: hg:Neighbourhood
        PPL: hg:Place
        CNL: hg:Water

    tgn:
      parents:
        - tgn:7007568
      relations:
        liesIn: hg:liesIn
        equivalence: hg:sameAs
      types:
        nations: hg:Country
        area: hg:Area
        canals: hg:Water
        channels: hg:Water
        general regions: hg:Region
        inhabited places: hg:Place
        provinces: hg:Province
        second level subdivisions: hg:Region
        neighborhoods: hg:Neighbourhood
        counties: hg:County
        boroughs: hg:Borough

import:
  dirs:
    - /path/to/spacetime/data/etl/transform
    - /path/to/spacetime/data/etl/infer

schemas:                                
  baseUri: http://rdf.spacetime.nypl.org

  baseType: PlaceInTime

  types:
    - hg:Address
    - hg:Building
    - hg:Street
    - hg:Neighbourhood
    - hg:Borough
    - hg:Ward
    - hg:State
    - hg:Place
    - hg:Municipality
    - hg:Region
    - hg:Water
    - hg:County
    - hg:Province
    - hg:Country
    - hg:Area

    - st:Cemetery
    - st:Person
    - st:Company
    - st:Photo
    - st:Map

  relations:
    - hg:sameAs
    - hg:liesIn

  equivalence: hg:sameAs    
```

## Services

In your `services` directory, clone the following repositories:

- https://github.com/nypl-spacetime/spacetime-api
- https://github.com/nypl-spacetime/spacetime-core

In each directory, run `npm install`.

## Tools

In your `tools` directory, clone the following repositories:

- https://github.com/nypl-spacetime/spacetime-etl
- https://github.com/nypl-spacetime/spacetime-import

In each directory, run `npm install`.

## Data

The Space/Time Directory needs data to run. In Space/Time's [GitHub organization](https://github.com/nypl-spacetime?utf8=%E2%9C%93&query=etl-), you can find a collection of [ETL](https://en.wikipedia.org/wiki/Extract,_transform,_load) modules which download data from external data sources, transform this data to the Space/Time data format, and do inference to find relations between different datasets.

Space/Time ETL modules [start with the `etl-` prefix](https://github.com/nypl-spacetime?utf8=%E2%9C%93&query=etl-).

- Clone the ones you need into your `etl-modules` directory.
- In each directory, run `npm install`

TODO: set `npm path`, add `spacetime/tools`! And install all ETL Modules with `npm production`.

## Create your first datasets
