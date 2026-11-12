# Threat model

## What this project does and where untrusted input enters
A recipe manager (Python/FastAPI backend + Vue frontend). Untrusted input: the HTTP API
(creating/editing recipes, importing from URLs), file uploads (images), and user auth. URL-based
import (SSRF) and file handling are the main surfaces.

## Components that matter most / least
- most: the API layer, the URL-import code (SSRF), and file-upload handling.
- less: the frontend, docs.

## How to exercise it
Import from crafted/hostile URLs (SSRF); upload crafted images; exercise the API with malformed
input.

## How you rate severity
- RCE or auth bypass: critical. SSRF reaching internal services: high. Path traversal: high.
  XSS: medium.

## Anything to leave alone
- The built frontend bundle is a build artifact; focus on the Python backend.
