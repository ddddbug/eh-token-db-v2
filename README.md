# eh-token-db-v2

A proposed successor to [eh-token-db](https://github.com/ddddbug/eh-token-db). This implementation provides a better solution since the crawler does not commit the SQL binary file via it any more, but it utilises a regular release of the binary file.

An automation crawler powered by GitHub Action, to collect `gid`
and `token` from e-hentai [RSS](https://xml.e-hentai.org/ehg.xml)
regularly. Temporary crawled data is cached in [data.txt](data.txt).

The latest data is released in [a SQLite3 database](https://github.com/ddddbug/eh-token-db-v2/releases/tag/latest). Nightly releases are available and organised by a month tag, thus a SQL dump text will be generated at the beginning of every month.

P.S. Each workflow run will cache two artifacts including a SQL binary and a dump, but they won't last long before cleaned by the 90-day retention policy. Well, the binary gets released anyway, so no need to panic.
