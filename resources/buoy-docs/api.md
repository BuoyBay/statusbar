---
title: "Status bar API"
summary: "Configure and own a desktop menu-bar or tray item with deterministic cleanup."
category: "Reference"
order: 20
keywords: ["statusbar", "status", "bar", "API", "lifecycle"]
symbols: ["StatusBarAvailable", "StatusBarActivation", "StatusBarController", "StatusBarController.Configure", "StatusBarController.Show", "StatusBarController.Hide", "StatusBarController.Close", "StatusBarController.IsVisible", "StatusBarController.IsClosed"]
related: ["index.md", "getting-started.md", "typed-api.md"]
---

# Status bar API

Import the `statusbar` package. Constructors below use the class name; invoke them with `New`. Listed members are public client APIs; native declarations and trampoline helpers are implementation details.

## Public surface

| Symbol | Contract |
| --- | --- |
| `StatusBarAvailable() As Boolean` | Checks desktop/session host availability without creating UI. |
| `StatusBarActivation` | Delegate Sub(tag As String, doubleClick As Boolean); provide AddressOf a module-level handler. |
| `StatusBarController(tag As String, handler As StatusBarActivation = Nil)` | Creates an inert configuration/lifetime object with a required tag. |
| `StatusBarController.Configure(toolTip As String, icon As Picture, menu As Optional Of Menu = None, iconName As String = "", templateIcon As Boolean = True)` | Stages or replaces pending/live presentation. Pass Some(menu) to attach a menu. |
| `StatusBarController.Show()` | Creates and shows on demand. A live item must have an icon or Linux theme name. |
| `StatusBarController.Hide()` | Temporarily hides without permanently closing the controller. |
| `StatusBarController.Close()` | Idempotently hides/removes native UI, disconnects callbacks, and releases ownership. |
| `StatusBarController.IsVisible As Boolean` | Read-only current item visibility. |
| `StatusBarController.IsClosed As Boolean` | Read-only permanent close state. |

## Ownership and timing

Construct, configure, show, hide, and close on the main thread. Retain the controller in its owning window and Close when the owner closes. Hide is temporary; Close permanently retires the controller. Worker-thread destruction queues main-thread cleanup, which requires a live application run loop. This package does not keep the process alive after its last window closes.

## Errors and result interpretation

A nonempty tag is required. Show fails when no tray host exists, and requires an icon (Linux also accepts an icon-theme name). Configure and Show reject a closed controller. Native compatibility checks can reject an incompatible Buoy macOS status-item record instead of using an unsafe native layout.

## Platform behavior

macOS uses template icons by default; Windows uses image colors. Linux requires a StatusNotifierItem host, with an extension on some GNOME configurations. Hosts can route all clicks to a menu instead of activation, and Linux has no double-click protocol. Check StatusBarAvailable before showing.

See the [complete usage example](getting-started.md) and the [package overview](index.md).


[Full typed API: properties, parameters, defaults, and returns](typed-api.md)
