# Prompt Efficiently for codex

Explicit rough input-token estimates and conservative prompt tightening. Not automatic agent metering. Same PE account, free quota and Pro entitlement as the website. No prompt text is sent to PE.

## Prerequisites and setup
Desktop, Python 3.10+, a secure OS credential store, and this folder. In your own terminal create a virtual environment and install the bundled requirements:

    python3 -m venv .venv
    .venv/bin/python -m pip install -r requirements.txt
    .venv/bin/python pe.py login

On Windows use `.venv\Scripts\python.exe`. On Linux a functioning Secret Service keyring is required; no insecure fallback is supported. Dependency downloads need internet. Python keyring is free software, not a paid service.

The email code is entered in your terminal only. Never paste it into Claude/Codex. Sessions use the OS credential store. Run `pe.py logout` to revoke. `pe.py status` checks quota/Pro. `pe.py upgrade` opens the PE website, where you sign in separately.

## Use
The helper reads only stdin, never your workspace. Pipe a prompt from your own trusted tool to `.venv/bin/python pe.py estimate` or `tighten`. Review suggestions before using them. A quota check can consume one free check even if the network drops after acceptance. New helper calls are new uses. Network/auth failures stop instead of bypassing the quota.

## Codex local plugin (tested with CLI 0.171.0)
From your own terminal, run:

    codex plugin marketplace add promptefficiently/pe-codex
    codex plugin add prompt-efficiently@pe-local
    codex plugin list

The install adds this repository as a marketplace. The test install recognizes this package and enables it without an AI inference request. Configure the helper Python path before use.

## Codex skill alternative
The folder has a portable plugin manifest and `skills/pe/SKILL.md`. For the simplest local skill install, copy the `skills/pe` directory under your personal `.agents/skills/` directory and keep pe.py plus requirements.txt alongside it. Restart Codex and explicitly invoke `$pe` with supplied prompt text. Set the helper virtual-environment Python path in your session. Portable local plugin installation varies by Codex surface/version.

## Limits and release gate
Rough word-based input tokens only, no output/context/tool cost or subscription-credit estimate.

Licence: MIT (see LICENSE). Sign-in, rewrites and billing run on Prompt Efficiently servers and are not part of this repository. Not affiliated with the AI products it supports.
