Been meaning to create a GarminIQ app (that runs on any head unit) that sends all the relevant data for IRL adventure/fitness streaming to a central server with an API that can be integrated with StreamElements and the like.

Device -> IQ app -> Connect phone app -> cloud server

## Requirements

- Ingest literally any data submitted with PUT
- Polling and SSE only (no websockets)
- Customizable forced latency setting
- Event timestamps required (NOT the time of the HTTP request)
- Events triggered for subscribing apps
- Also add regular/polling intervals for common backend queries

## Generic data ingestion and consolidation

The main service required is something that will take any structured data, consolidate it, and allow it to be queried in different ways.

- Endpoint path agnostic (the URL path becomes part of the data, https://example.com/rwxrob/put)
- HTTP MIME headers
- QueryString

Query it with simple HTTP GET polling and server-sent events (SSE).
## Questions

*What about Xert?*

PeloTom famously integrated Xert data on the screen, but this requires Xert. It does, however, prove that a GarminIQ app can send anything available from any Garmin device that supports GarminIQ up to something on the Internets.

*Do we use websockets or not?*

