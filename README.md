# falcon-evidence

Public host for Falcon QA evidence — screenshots and repro artifacts referenced from issues in private `matty-v/*` repos.

## Why this exists

GitHub renders inline images in issue markdown via its camo proxy, which fetches the image URL unauthenticated. For source repos that are private, raw URLs return 404 to camo and the image renders broken. The only way to inline evidence in a private-repo issue without using the web UI's drag-drop is to host the asset somewhere camo can reach anonymously — i.e. a public repo.

## Conventions

- Filename: `<source-repo>-<issue#>-<slug>.<ext>` (e.g. `kyber-355-status-pane.png`)
- All assets live at the repo root. No directories.
- Reference from an issue body via:

  ```markdown
  ![desc](https://raw.githubusercontent.com/matty-v/falcon-evidence/main/<file>)
  ```

## Lifecycle

Evidence is tied to the issue that references it. When the issue closes, the corresponding evidence file should be deleted in the same PR (or a follow-up hygiene pass).

## Redaction policy

This repo is **public**. Anything pushed here is world-readable forever (git history retains deleted blobs). Before pushing, evidence must be scrubbed of:

- API keys, tokens, bearer headers
- Internal IPs and hostnames not already in public DNS
- User/customer PII
- Anything that would be embarrassing in a search result

If a screenshot can't be safely redacted, host it on the boba-fett pod and reference it textually rather than inlining.

## Who writes here

Push access is restricted to `matty-v` (owner) and the Falcon QA agent (Boba Fett), which runs under the owner's PAT. No other collaborators.

## Who reads here

The world (it's public). That's the point — anonymous camo fetches need to succeed.
