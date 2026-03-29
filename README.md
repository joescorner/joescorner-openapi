# Joe's Corner OpenAPI Specification

This repository contains the [OpenAPI 3.1.0](https://spec.openapis.org/oas/v3.1.0) specification for the [Joe's Corner](https://joescorner.ai) public REST API.

The API is read-only, requires no authentication, and is available at `https://api.joescorner.ai`.

The specification is available in [`openapi.json`](openapi.json) and [`openapi.yaml`](openapi.yaml).

[Changelog](CHANGELOG.md)

> The API is subject to change at any time.


## Endpoints

- `GET /v1/feeds` -- List public feeds (paginated, sortable)
- `GET /v1/feeds/{username}/{feed_slug}` -- Get a single feed with sources and preferences
- `GET /v1/feeds/{username}/{feed_slug}/posts` -- List posts for a feed (paginated)
- `GET /v1/feeds/{username}/{feed_slug}/posts/{post_id}` -- Get a single post


## Quick start

List the most popular feeds:

```sh
curl https://api.joescorner.ai/v1/feeds
```

Get the latest posts from a feed:

```sh
curl https://api.joescorner.ai/v1/feeds/joescorner/us-stock-market/posts
```

Paginate through results using the `next_cursor` value from a previous response:

```sh
curl "https://api.joescorner.ai/v1/feeds?cursor=<next_cursor value>"
```


## Pagination

Paginated endpoints use cursor-based pagination.

- `limit` controls the page size (max 100, defaults vary by endpoint).
- Responses include a `next_cursor` field when more results are available.
- Pass `next_cursor` as the `cursor` query parameter to fetch the next page.
- When `next_cursor` is absent, there are no more results.


## Response headers

All responses include the following headers:

- `API-Version` -- Semantic version of the API (currently `1.0.0`)
- `Cache-Control` -- Cache directive (currently `public, max-age=120`)


## Versioning

The API is versioned via the URL path prefix (`/v1/`). 
The `API-Version` response header reflects the current semantic version within that major version. 
The `info.version` field in the spec matches the `API-Version` header.


## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md).


## License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.
