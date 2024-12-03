## GitHub Copilot Chat

- Extension Version: 0.22.4 (prod)
- VS Code: vscode/1.95.3
- OS: Windows

## Network

User Settings:
```json
  "github.copilot.advanced": {
    "debug.useElectronFetcher": true,
    "debug.useNodeFetcher": false
  }
```

Connecting to https://api.github.com:
- DNS ipv4 Lookup: 140.82.113.5 (9 ms)
- DNS ipv6 Lookup: Error: getaddrinfo ENOTFOUND api.github.com
- Electron Fetcher (configured): HTTP 200 (275 ms)
- Node Fetcher: HTTP 200 (856 ms)
- Helix Fetcher: HTTP 200 (1455 ms)

Connecting to https://api.individual.githubcopilot.com/_ping:
- DNS ipv4 Lookup: 140.82.113.22 (47 ms)
- DNS ipv6 Lookup: Error: getaddrinfo ENOTFOUND api.individual.githubcopilot.com
- Electron Fetcher (configured): HTTP 200 (695 ms)
- Node Fetcher: HTTP 200 (357 ms)
- Helix Fetcher: HTTP 200 (333 ms)

## Documentation

In corporate networks: [Troubleshooting firewall settings for GitHub Copilot](https://docs.github.com/en/copilot/troubleshooting-github-copilot/troubleshooting-firewall-settings-for-github-copilot).