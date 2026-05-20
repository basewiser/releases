# Basewiser Releases

Public release registry for [Basewiser](https://basewiser.com) — a self-hosted Entra ID security toolkit for MSPs.

This repository contains **only release metadata and deployment artifacts**:

| File | Purpose |
|---|---|
| `latest.json` | Current portal + backend version pointer |
| `deploy/update.json` | ARM template the in-portal "Update" button deploys |
| `notes/` | Per-release changelogs (when present) |

**Source code is private.** Customers deploy Basewiser using container images published to GHCR — the source itself lives in a private repository.

## How it's used

Each customer's portal periodically fetches `latest.json` from this repo. When a newer release is available than the one currently deployed, the portal shows an in-app update banner. Clicking "Update in Azure Portal" opens an Azure Custom Deployment pre-filled with the new image tag — the customer reviews the deployment and clicks Apply in their own Azure subscription.

Nothing in this repo runs on the customer's side. It's just JSON and ARM templates served via GitHub's raw CDN.

## Versioning

Tags follow the pattern `portal-vYYYYMMDD.HHMMSS` and `backend-vYYYYMMDD.HHMMSS`. The portal compares the bundled-in version constant to `latest.json.portal.tag` lexicographically.

## Distribution

| Surface | Location |
|---|---|
| Portal image | `ghcr.io/basewiser/portal:<tag>` |
| Backend image | `ghcr.io/basewiser/portal-backend:<tag>` (when applicable; backend is currently zip-deployed) |
| ARM template | `https://raw.githubusercontent.com/basewiser/releases/main/deploy/update.json` |
| Version manifest | `https://raw.githubusercontent.com/basewiser/releases/main/latest.json` |

## License

Content in this repo (metadata + ARM template) is MIT-licensed. The Basewiser product itself is proprietary and requires a license to use.
