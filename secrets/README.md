# Secrets

This directory holds Docker Secret files for Bragi's Bots. These files are **never committed to git**.

## Required Secrets

| Filename | Description |
|---|---|
| `prism_fluxer_token` | Bot token from the Fluxer Developer Portal for Prism |
| `portia_fluxer_token` | Bot token from the Fluxer Developer Portal for Portia |

## Setup

Create each secret file with no trailing newline:

```
printf 'your-token-here' > ./secrets/prism_fluxer_token
printf 'your-token-here' > ./secrets/portia_fluxer_token
```
