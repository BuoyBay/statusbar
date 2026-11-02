# statusbar · 0.1.0

Lifecycle-managed menu bar / tray items built on Buoy's existing native
`StatusItem`. `Import statusbar`. This adds deferred creation, consistent
configuration, routing by tag, availability checks and deterministic close.

| API | Behavior |
| --- | --- |
| `StatusBarAvailable()` | Checks desktop/session host support before creating UI. |
| `New StatusBarController(tag, handler = Nil)` | Inert configuration object; no tray item yet. |
| `Configure(toolTip, icon, menu As Optional Of Menu = None, iconName = "", templateIcon = True)` | Configure or replace both pending and live presentation. Pass `Some(menu)` to attach a menu. |
| `Show()` / `Hide()` | Create/show on demand or temporarily hide. An icon is required (Linux also accepts an icon-theme name). |
| `Close()` | Idempotently hides/removes the item, disconnects callbacks and releases native ownership. A closed item cannot be resurrected. |
| `IsVisible` / `IsClosed` | Read-only lifecycle state. |

`StatusBarActivation` is a delegate Sub taking `(tag As String, doubleClick As
Boolean)`. Supply `AddressOf` a module-level handler; the tag distinguishes
instances without a global current-item pointer. Double click also includes the
native preceding primary click on macOS. Menu actions use the existing
`Menu.SetOnSelected` callback; register it on your menu before passing `Some(menu)`.

Construct/configure/show/hide/close on the main thread. Keep the controller alive
while its item is visible and close it in its owning window's Closed handler.
The destructor explicitly queues native cleanup on the main thread when a worker
releases the last reference; explicit Close remains preferable. The application
run loop must still be running to drain queued cleanup.

macOS uses native template images by default (pass `templateIcon: False` for color
artwork). Windows renders the actual colors. Linux uses StatusNotifierItem;
GNOME needs a compatible host/extension, detected by `StatusBarAvailable`. A Linux
host can route every click to the menu instead of invoking activation, and there
is no Linux double-click protocol. The package cannot turn a normal app into a
menu-bar-only process or keep Buoy alive after its last window closes.
