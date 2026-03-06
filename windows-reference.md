# Yahoo! Messenger Windows Reference

> All skinnable windows and their XML sources, excluding IMWindow-based windows.

## Window Frame Types (theme.xml)

Every window uses one of three frame styles defined in `theme/theme.xml`:

| Frame Style | Image File | Used By |
|---|---|---|
| `mainframewindow` | `mainframewindow.png` | Main buddy list window |
| `framewindow` | `framewindow.png` | IM/chat windows, other captioned windows |
| `toolwindow` | `toolwindow.png` | Popups, tool dialogs, layered windows |

---

## Non-IMWindow Sections

### FriendList.xml — `FriendList/FriendList.xml`

Contains **3 sections**:

| Section ID | Description | Frame | Resizable | Caption |
|---|---|---|---|---|
| `FriendList` | Main buddy list window | `mainframewindow` | Yes | Yes |
| `GoMobileWnd` | "Go Mobile" popup for call/IM forwarding | `toolwindow` | No | No |
| `SkinPickerWnd` | Skin picker popup (thumbnail grid) | `toolwindow` | No | No |

### ContactCard.xml — `ContactCard/ContactCard.xml`

Contains **3 sections**:

| Section ID | Description | Frame | Resizable | Caption |
|---|---|---|---|---|
| `ContactCard` | Hover card for a buddy (actions, status, avatar) | None (layered popup) | No | No |
| `MyContactCard` | Hover card for local user (profile, account links) | None (layered popup) | No | No |
| `ContactCardOverlay` | Floating action buttons overlay on buddy list | None (layered/composited) | No | No |

### AddRequest.xml — `AddRequest/AddRequest.xml`

| Section ID | Description | Frame | Resizable | Caption |
|---|---|---|---|---|
| `MultiAddRequest` | Multi-add buddy request dialog | `framewindow` | No | Yes |

### MiscSmallUI.xml — `MiscSmallUI/MiscSmallUI.xml`

| Section ID | Description | Frame | Resizable | Caption |
|---|---|---|---|---|
| `OfflineMsgViewer` | Offline message viewer window | `framewindow` | Yes | Yes |

### sumo.xml — `sumo/sumo.xml`

| Section ID | Description | Frame | Resizable | Caption |
|---|---|---|---|---|
| `sumo` | Yahoo! Messenger All-Stars award dialog | `framewindow` | No | Yes |

### SlotManagerControls.xml — `SlotManager/SlotManagerControls.xml`

| Section ID | Description | Frame | Resizable | Caption |
|---|---|---|---|---|
| `SlotManagerControls` | Plugin slot manager controls (add/up/down) | None (embedded panel) | No | No |

### Y!Msgr.xml — `Y!Msgr.xml`

Contains **3 sections** (legacy/internal layout definitions):

| Section ID | Description | Frame | Caption |
|---|---|---|---|
| `MainWindow` | Main window layout (alternate/legacy) | `mainframewindow` | Yes |
| `main` | Internal debug/test layout | `mainframewindow` | Yes |
| `chat` | Internal debug/test chat layout | `framewindow` | Yes |

> **Note:** `Y!Msgr.xml` appears to be a legacy or internal file. The actual buddy list layout is in `FriendList/FriendList.xml` and IM layout in `IMWindow/IMWindow.xml`.

---

## IMWindow-Based Sections (for completeness)

These are in `IMWindow/IMWindow.xml` and are **not** covered here:

| Section ID | Description |
|---|---|
| `IMWindow` | IM conversation window |
| `ConvSidePanel` | Conversation side panel (plugins, photo sharing) |

---

## About Window & Other System Dialogs

The **About** window, **Preferences**, **File Transfer**, and similar system dialogs are **not skinnable** through section XML files. They use the `framewindow` or `toolwindow` frame from `theme.xml` but their internal layout is hardcoded in the application.

What you **can** control for these windows:
- Window frame appearance → `framewindow` / `toolwindow` style in `theme.xml`
- Button styles → `pushbutton` style in `theme.xml`
- Colors → `colors.xml` (system color overrides like `window_frame`, `backcolor`)
- Scrollbars, checkboxes, etc. → corresponding styles in `theme.xml`
