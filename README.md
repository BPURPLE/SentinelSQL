# SentinelSQL

SentinelSQL is an AI-assisted SQL security gateway MVP.

## Architecture

The permitted request flow is:

`gateway -> detection -> decision -> response/logging`

The gateway intercepts database requests. Detection produces evidence only; the decision layer alone authorizes `ALLOW` or `BLOCK`. Explainability can describe a completed decision but cannot influence it.

See [architecture documentation](docs/architecture/README.md) and [security documentation](docs/security/README.md).
