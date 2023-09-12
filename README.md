# eh-token-db-v2

A proposed successor to [eh-token-db](https://github.com/ddddbug/eh-token-db). 

## Motivation

The previous implementation commits the SQL binary file via git every 30 minutes. Consequently, the computing power to commit the binary file repeatedly grows rapidly with regard to the size of the binary file and the number of repeats. After running for 19 months and committing over 24k times, the old workflow now needs about 28 minutes to complete, and its fail rate recently spikes to 50%. It won't be long before the previous workflow completely stops running thus it's wasting too much time and computing power.

Time to move forward!

This updated implementation provides a better solution by avoiding committing binary files, and instead, utilising a regular release of the binary file. This should slow down the growth of the project's size (since only the cached text file `data.txt` is being committed regularly) and optimise the workflow running time to a constant level. Well, we will see.

\* If `v2` is eventually failing, the next step is to get rid of committing any files, and just utilise release...

## Description

An automation crawler powered by GitHub Action, to collect `gid`
and `token` from e-hentai [RSS](https://xml.e-hentai.org/ehg.xml)
regularly. Temporary crawled data is cached in [data.txt](data.txt).

The [`get` workflow](.github/workflows/get.yml) releases the latest data every 30 minutes in [a SQLite3 database](https://github.com/ddddbug/eh-token-db-v2/releases/tag/latest). So does it release the database "nightly" and organise nightly builds by a month tag.
The [`release` workflow](.github/workflows/release.yml) releases the database with a SQL dump text at the beginning of every month.

P.S. Each workflow run will cache two artifacts including a SQL binary and a dump, but they won't last long before cleaned by the 90-day retention policy. Well, the binary gets released anyway, so no need to panic.
