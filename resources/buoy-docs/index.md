---
title: "Status bar"
summary: "Configure and own a desktop menu-bar or tray item with deterministic cleanup."
category: "Overview"
order: 0
keywords: ["statusbar", "status", "bar"]
related: ["getting-started.md", "api.md", "typed-api.md"]
---

# Status bar

StatusBarController adds deferred creation, tag-based activation routing, and explicit lifetime management above Buoy StatusItem. Construction is inert; Show creates the native item only when needed.

## Platform support

macOS uses template icons by default; Windows uses image colors. Linux requires a StatusNotifierItem host, with an extension on some GNOME configurations. Hosts can route all clicks to a menu instead of activation, and Linux has no double-click protocol. Check StatusBarAvailable before showing.

## Start reading

- [Getting started](getting-started.md) walks through installation and a complete example.
- [API reference](api.md) describes public symbols, state, errors, and ownership.

## Scope

Construct, configure, show, hide, and close on the main thread. Retain the controller in its owning window and Close when the owner closes. Hide is temporary; Close permanently retires the controller. Worker-thread destruction queues main-thread cleanup, which requires a live application run loop. This package does not keep the process alive after its last window closes.
