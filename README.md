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

By default, Space/Time uses the default ports, users and passwords for all databases. To override this, edit your configuration file.

## configuration

```yml
api:
  dataDir: /path/to/spacetime/data
  admin:
    name: spacetime
    password: password
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

The Space/Time Directory needs data to run. In Space/Time's GitHub organization, you can find a large collection of [ETL](https://en.wikipedia.org/wiki/Extract,_transform,_load) modules which download data from external data sources, transform this data to the Space/Time data format, and do inference to find relations between different datasets.

Space/Time ETL modules [start with the `etl-` prefix](https://github.com/nypl-spacetime?utf8=%E2%9C%93&query=etl-).

- Clone the ones you need into your `etl-modules` directory.
- In each directory, run `npm install`
