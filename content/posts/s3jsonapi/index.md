---
title: "s3jsonapi"
date: 2026-03-29T12:00:00Z
summary: "s3jsonapi is a simple HTTP server that exposes an S3-compatible bucket as a JSON key/value API."
og_image: "https://johnritsema.com/posts/s3jsonapi/s3jsonapi.png"
---

I've been running [s3jsonapi](https://github.com/jritsema/s3jsonapi) quietly for a few years now on top of [Minio](https://min.io/) for some of my home projects. It's a small HTTP server that exposes an [S3-compatible bucket](https://docs.aws.amazon.com/AmazonS3/latest/API/API_Operations_Amazon_Simple_Storage_Service.html) as a simple JSON key/value API (PUT, GET, DELETE, and list). No database, no schema, just JSON blobs stored by key.

I decided to open source it recently after finding a new use for it: giving AI agents a simple persistence layer. When building agentic workflows, you often need somewhere to store state, memory, or intermediate results without standing up a full database. If S3 is already in the stack (or you're running Minio locally), this gives agents a clean HTTP interface they can read and write with no extra infrastructure.

## How it works

Keys map directly to S3 object paths. A PUT to `/prefix/key` stores the JSON body at `s3://bucket/prefix/key`. A GET to `/prefix/` lists all keys under that prefix, with an optional `?expand=1` to eagerly fetch and return the full contents of all keys as a JSON array.

```sh
# write
curl -X PUT http://localhost:8080/session/abc123 -d '{"step":"research","status":"complete"}'

# read
curl http://localhost:8080/session/abc123
# {"step":"research","status":"complete"}

# list
curl http://localhost:8080/session/
# {"keys":["abc123"]}
```

It works with [AWS S3](https://aws.amazon.com/s3/) and any S3-compatible API including [Minio](https://min.io/), [Backblaze B2](https://www.backblaze.com/cloud-storage), [Cloudflare R2](https://www.cloudflare.com/developer-platform/r2/), and others.

There's no authentication, so it's best suited for local development, internal tooling, or private network deployments. Check out the [repository](https://github.com/jritsema/s3jsonapi) for configuration and usage details.
