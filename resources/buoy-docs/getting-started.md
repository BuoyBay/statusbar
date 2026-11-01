---
title: "Status bar getting started"
summary: "Install statusbar and use its core API with explicit application ownership."
category: "Guides"
order: 10
keywords: ["statusbar", "status", "bar", "installation", "example"]
related: ["index.md", "api.md", "typed-api.md"]
---

# Status bar getting started

## Install and import

Copy the sealed `statusbar-0.1.0.buipkg` archive into your project `packages/` directory, or install a source/registry dependency named `statusbar` using BPM and sync it. Then use `Import statusbar`. The archive includes this documentation as package resources.

Use a consuming source filename such as `main.bui`; a local module named exactly like the package shadows its import.

## Complete usage example

The example is compiler-checked as a complete Buoy module. Functions and Subs are intended to be called from the consuming app at the appropriate user action or lifecycle event.

```buoy
Import statusbar

Function ShowApplicationStatus(icon As Picture) As StatusBarController
    If Not StatusBarAvailable() Then Return Nil
    Dim controller As New StatusBarController("application-status")
    controller.Configure("Application status", icon)
    controller.Show()
    Return controller
End Function
```

## Integrate with the application

Construct, configure, show, hide, and close on the main thread. Retain the controller in its owning window and Close when the owner closes. Hide is temporary; Close permanently retires the controller. Worker-thread destruction queues main-thread cleanup, which requires a live application run loop. This package does not keep the process alive after its last window closes.

## Activation and menus

Supply AddressOf a module-level StatusBarActivation handler when constructing a controller. Its tag distinguishes instances, and its doubleClick flag includes the preceding primary-click event on macOS. Register Menu.SetOnSelected on a menu before passing Some(menu) to Configure. Linux hosts may open the menu for every click rather than delivering an activation callback. Keep the returned controller in an owner property and Close it from that owner's Closed handler.

## Handle failures and unsupported targets

A nonempty tag is required. Show fails when no tray host exists, and requires an icon (Linux also accepts an icon-theme name). Configure and Show reject a closed controller. Native compatibility checks can reject an incompatible Buoy macOS status-item record instead of using an unsafe native layout.

macOS uses template icons by default; Windows uses image colors. Linux requires a StatusNotifierItem host, with an extension on some GNOME configurations. Hosts can route all clicks to a menu instead of activation, and Linux has no double-click protocol. Check StatusBarAvailable before showing.

Return to the [overview](index.md) or consult the [API reference](api.md).
