# renovate
Renovate configuration

## usage

- renovate.json

```json
{
    "extends": ["github>imagica-et/renovate"]
}
```

- package.json

```json
{
  "name": "renovate-config-fastcore",
  "version": "0.0.1",
  ...
  "renovate-config": {
    "default": {
      "extends": ["github>imagica-et/renovate"]
    }
  }
}
```
