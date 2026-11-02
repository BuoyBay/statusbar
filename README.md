# Menu-bar and tray status items

Lifecycle-managed menu bar / tray items built on the existing native
`StatusItem`. `Import statusbar`. This adds deferred creation, consistent
configuration, routing by tag, availability checks and deterministic close.

`StatusBarActivation` is a delegate Sub taking `(tag As String, doubleClick As
Boolean)`. Supply `AddressOf` a module-level handler; the tag distinguishes
instances without a global current-item pointer. Double click also includes the
native preceding primary click on macOS. Menu actions use the existing
`Menu.SetOnSelected` callback; register it on your menu before passing `Some(menu)`.

## Install

From a Buoy consumer project with BPM installed:

```sh
bpm add statusbar --git https://github.com/BuoyBay/statusbar.git --rev refs/heads/main
```

BPM records the resolved commit in its lockfile. Keep that lockfile with the
consumer project for reproducible installs.

## Example

```basic
Import statusbar

Function ShowApplicationStatus(icon As Picture) As StatusBarController
    If Not StatusBarAvailable() Then Return Nil
    Dim controller As New StatusBarController("application-status")
    controller.Configure("Application status", icon)
    controller.Show()
    Return controller
End Function
```

## Build from source

With the native `build-packages` driver from [devtools](https://github.com/BuoyBay/devtools)
on your `PATH`, run from this checkout:

```sh
build-packages --root "$PWD" --compile-consumer statusbar
```

The driver checks source targets and compiles an import consumer. See the
[API guide](docs/API.md) for behavior, limits and any host prerequisites.

## Local Buoy setup

On your own machine, install Buoy and run:

```sh
buoy ai init --both
```

## Contributing

[Contributing](CONTRIBUTING.md) · [License](LICENSE)
