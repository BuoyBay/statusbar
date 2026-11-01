---
title: "statusbar typed API"
summary: "Source-derived public signatures, properties, parameters, defaults, and return values."
category: "Reference"
order: 21
types: ["StatusBarActivation", "StatusBarController"]
dependencies: []
symbols: ["StatusBarActivation", "StatusBarController"]
related: ["api.md", "getting-started.md", "index.md"]
---

# statusbar typed API

Generated from the package source declarations. Platform guards are shown where present; inherited members are documented on the base type. See the [API contracts](api.md) for behavior and limitations.

## StatusBar functions

### StatusBarActivation

`Public Delegate Sub StatusBarActivation(tag As String, doubleClick As Boolean)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `tag` | `String` | `ByVal` | Required |
| `doubleClick` | `Boolean` | `ByVal` | Required |

Returns: no value.

### StatusBarAvailable

`Public Function StatusBarAvailable() As Boolean`

No parameters.

#### Returns

| Type |
| --- |
| `Boolean` |

## StatusBarController

`Public Class StatusBarController`

Construction is inert; Show creates the native item. Close releases its native resources.

### Properties

| Name | Type | Read-Only | Shared | Default | Description |
| --- | --- | --- | --- | --- | --- |
| `IsVisible` | `Boolean` | Yes | No | — | — |
| `IsClosed` | `Boolean` | Yes | No | — | — |

### Constructor

`Public Sub Constructor(tag As String, handler As StatusBarActivation = Nil)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `tag` | `String` | `ByVal` | Required |
| `handler` | `StatusBarActivation` | `ByVal` | `Nil` |

Returns: no value.

### Configure

`Public Sub Configure(toolTip As String, icon As Picture, menu As Optional Of Menu = None, iconName As String = "", templateIcon As Boolean = True)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `toolTip` | `String` | `ByVal` | Required |
| `icon` | `Picture` | `ByVal` | Required |
| `menu` | `Optional Of Menu` | `ByVal` | `None` |
| `iconName` | `String` | `ByVal` | `""` |
| `templateIcon` | `Boolean` | `ByVal` | `True` |

Returns: no value.

### Show

`Public Sub Show()`

No parameters.

Returns: no value.

### Hide

`Public Sub Hide()`

No parameters.

Returns: no value.

### Close

`Public Sub Close()`

No parameters.

Returns: no value.

### Destructor

`Public Sub Destructor()`

No parameters.

Returns: no value.
