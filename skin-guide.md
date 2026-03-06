# How to Make a Yahoo! Messenger Skin

A step-by-step guide to creating your own Yahoo! Messenger skin. The easiest way to get started is to **copy an existing skin and modify it** — this guide walks you through exactly that.

---

## How Skins Work

Every skin **inherits from the Default skin**. You only need to include files that you want to change — anything you leave out automatically falls back to Default. This means a skin can be as simple as a single `colors.xml` file, or as detailed as a fully custom theme with artwork.

The **Ruby Red - Teto** skin in this repo is the most complete example — it customizes nearly every element and is the best starting point for a full skin. **Icy Blue - Hatsune Miku** is a lighter example that overrides fewer things.

---

## Skin Folder Structure

Here's what a fully-featured skin looks like (based on Ruby Red - Teto, the most complete skin in this repo):

```
My Awesome Skin/
├── colors.xml              ← REQUIRED: Your color palette
├── Localized.xml           ← REQUIRED: Display name in skin picker
├── preview.png             ← Skin picker thumbnail (~150x200px)
│
├── theme/
│   ├── theme.xml           ← Window frame styling
│   ├── mainframewindow.png ← Buddy list window frame
│   ├── framewindow.png     ← IM window frame
│   ├── toolwindow.png      ← Popup window frame
│   ├── framewindow.rgn     ← Window shape
│   ├── mainframewindow.rgn
│   ├── toolwindow.rgn
│   ├── Yahoo!_Messenger.png ← Logo in title bar
│   ├── ellipsis.png        ← Title bar ellipsis
│   ├── menubar.png         ← Menu bar background
│   ├── menuitem.png        ← Menu dropdown item background
│   ├── menu_bg.png         ← Menu background
│   ├── headerbg.png        ← List header background
│   ├── pushbuttons.png     ← Button sprites (6 states)
│   ├── grabber.png         ← Grabber handle
│   ├── tabs.png            ← Tab control sprites
│   ├── slotborder*.png     ← Plugin slot borders
│   ├── scroll_*.png        ← Scrollbar images
│   ├── checkbox.bmp        ← Custom checkbox
│   └── radio.bmp           ← Custom radio button
│
├── images/
│   ├── bg_hover.png        ← List item hover highlight
│   ├── bg_selected.png     ← List item selected highlight
│   ├── btn-single-*.png    ← Various button images
│   ├── btn-middle-small.png
│   ├── btn-right-small.png
│   └── resize_ctrl.png     ← Window resize grip
│
├── FriendList/
│   ├── FriendList.xml      ← Buddy list layout overrides
│   ├── me_bg.png           ← "Me" panel background (~169x61)
│   ├── SearchBar.png       ← Search bar (normal)
│   ├── SearchBar_h.png     ← Search bar (hover)
│   ├── SearchBar_fc.png    ← Search bar (focused)
│   ├── SearchBarButton.png ← Search bar button
│   ├── btn-single-status.png ← Status button
│   ├── DisplayImgOverlay.png
│   ├── AddBuddyPanel.png
│   ├── PluginPanel.png     ← Plugin panel images
│   ├── PluginPanelFiller.png
│   └── BottomPluginEdge.png
│
├── IMWindow/
│   ├── IMWindow.xml        ← IM window layout overrides
│   ├── toolbar_back.png    ← IM toolbar background (~200x44)
│   └── im_tb_*.png         ← IM toolbar button images
│
├── ContactCard/            ← Contact card images
│   ├── background.png
│   ├── Frame.png
│   ├── CallButton.png
│   └── SmsButton.png
│
├── SlotManager/            ← Plugin slot images
│   └── BottomPluginPanel.png
│
└── sumo/                   ← Game/mini-app images
    └── background.png, etc.
```

You **don't need all of these**. Ruby Red includes every possible override, but you can start with just the basics and add more later. Files you leave out simply fall back to Default.

---

## Step 1: Copy an Existing Skin

The easiest way to start is to **duplicate an existing skin** and modify it:

1. **Copy the `Ruby Red - Teto (FB)` folder** from `VOCALOID SKINS SET/` — it has the most complete set of files and is the best base for a fully customized skin
2. **Rename the copied folder** to your skin's name (e.g., `My Awesome Skin`)
3. You now have a working skin with every file already in place

> If you want a simpler starting point, copy **Icy Blue - Hatsune Miku** instead — it overrides fewer things and is easier to understand, but won't cover as many UI elements.

---

## Step 2: Set Your Skin Name (Localized.xml)

Open `Localized.xml` and change the display name:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<theme LocalizedName="My Awesome Skin">
</theme>
```

This is the name shown in the Yahoo! Messenger skin picker.

---

## Step 3: Customize Colors (colors.xml)

This is where you define your skin's entire color palette. Open `colors.xml` — if you copied Ruby Red, you'll see it's organized into two sections:

- **`<colors>`** — skin-specific colors (hex `"RRGGBB"` or decimal `"R,G,B"`)
- **`<syscolors>`** — Windows system color overrides (**must** use decimal `"R,G,B"` format)

### Key Colors to Change First

These are the most impactful colors — change these and your skin will already look entirely different:

| Color ID | What it controls | Ruby Red value |
|---|---|---|
| `mainwndbackcolor` | Main background (Me panel, IM window) | `133,3,35` |
| `back` | Login panel, search background | `133,3,35` |
| `backcolor` | Additional background areas | `133,3,35` |
| `text` | Default body text | `cccccc` |
| `defaulttextcolor` | IM window user ID text | `f3f3f3` |
| `activemaincaption` | Title bar text (active) | `f3f3f3` |
| `widget_group_header` | Buddy list group name color | `9d4a5e` |
| `selection` | Highlight/selection background | `9d4a5e` |
| `control_fb` | Focused control background (prefs title) | `9d4a5e` |
| `dialog` (syscolor) | Dialog/login panel background | `133,3,35` |

### Color Scheme Strategy

Pick **one primary color** and derive your palette from it:

- **Background colors** (`mainwndbackcolor`, `back`, `backcolor`, `dialog`) → your primary color
- **Accent colors** (`widget_group_header`, `selection`, `control_fb`) → a lighter/different shade of your primary
- **Text colors** → high contrast against backgrounds (light text on dark BG, or dark text on light BG)
- **Menu item text** (`menuitem`) → keep dark since dropdown menus usually have light backgrounds

> **Tip:** Use the template [colors.xml](colors.xml) in this repo for a complete list of every color ID with dark/light examples.

**At this point, your skin already looks different!** Install it (see Step 7) to preview your color changes. Everything below customizes images and layout.

---

## Step 4: Customize Window Frames (theme.xml)

Open `theme/theme.xml` to control window borders, title bars, and UI controls.

The frame images are PNG files that define the borders around each window type. These use a **9-slice grid system** (`resizemargin`) so they scale without stretching your artwork.

### How resizemargin Works

```
resizemargin="left, top, right, bottom"
```

This splits your image into a grid. The **corners stay fixed**, and the **center tiles** to fill the space:

```
┌──────────┬─────────────────────────┬──────────┐
│  FIXED   │      TILES/STRETCHES    │  FIXED   │
│  (left)  │                         │  (right) │
├──────────┼─────────────────────────┼──────────┤
│          │                         │          │
│  TILES   │      TILES/STRETCHES    │  TILES   │
│          │                         │          │
├──────────┼─────────────────────────┼──────────┤
│  FIXED   │      TILES/STRETCHES    │  FIXED   │
│ (bottom) │                         │ (bottom) │
└──────────┴─────────────────────────┴──────────┘
```

**Place character artwork in the FIXED sections** (they won't stretch). Use a simple tileable color in the stretch sections.

### Adding Artwork to the Title Bar

Use directional resizemargin to reserve space for artwork:

```xml
resizemargin_top="10,0,170,0"
```

- `10` — 10px fixed on the left
- `0` — no stretch/tile in the middle
- `170` — **170px reserved on the right for your artwork**
- `0` — unused

### Ruby Red's theme.xml (Full Example)

Here's what Ruby Red uses — it defines `<style>` blocks that **completely replace** the Default styles, giving maximum control:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<theme>
<styles>
  <!-- Main buddy list window frame -->
  <style id="mainframewindow"
      imagefile="mainframewindow.png"
      logo="Yahoo!_Messenger.png"
      ellipsis="ellipsis.png"
      resizemargin="4,44,4,5"
      resizemargin_top="10,0,170,0"
      resizemargin_bottom="3,0,9,0"
      resizemargin_left="0,0,0,9"
      resizemargin_right="0,0,0,9"
      active_font="defaultfontbold" active_textcolor="activemaincaption"
      inactive_font="defaultfontbold" inactive_textcolor="itactivemaincaption"
      icon_xpos="10" icon_ypos="7"
      title_xpos="-100" title_ypos="-100"/>

  <!-- IM/chat window frame -->
  <style id="framewindow"
      imagefile="framewindow.png"
      resizemargin="3,28,2,4"
      resizemargin_top="10,0,170,0"
      resizemargin_bottom="0,0,9,0"
      resizemargin_left="0,1,0,9"
      resizemargin_right="0,1,0,9"
      active_font="defaultfontbold" active_textcolor="activemaincaption"
      inactive_font="defaultfontbold" inactive_textcolor="itactivemaincaption"
      icon_xpos="10" icon_ypos="6"
      title_xpos="30" title_ypos="0"/>

  <!-- Popup/tool windows -->
  <style id="toolwindow"
      imagefile="toolwindow.png"
      resizemargin="2,17,2,3"
      resizemargin_top="13,0,13,0"
      resizemargin_bottom="3,0,3,0"
      resizemargin_left="0,1,0,3"
      resizemargin_right="0,1,0,3"
      active_font="defaultfontnormal" active_textcolor="activecaption"
      inactive_font="defaultfontnormal" inactive_textcolor="itactivecaption"
      icon_xpos="5" icon_ypos="5"
      title_xpos="24" title_ypos="3"/>

  <!-- Menu bar styling -->
  <style id="menu"
      imagefile="menu_bg.png"
      imagefile_menuitem="menuitem.png"
      imagefile_mainbaritem="mainmenubar.png"
      imagefile_baritem="menubar.png"
      resizemargin_baritem="4,0,91,0" />

</styles>
</theme>
```

### What to Modify

If you copied Ruby Red, you mostly just need to **replace the image files** with your own artwork. The XML values usually stay the same unless you're changing artwork dimensions:

- **Replace `mainframewindow.png`** — your buddy list window border (~190x128px)
- **Replace `framewindow.png`** — your IM window border (~190x192px)
- **Replace `toolwindow.png`** — popup window border (~97x74px)
- **Replace `Yahoo!_Messenger.png`** — title bar logo (~161x34px)
- **Adjust `resizemargin_top` right value** if your artwork width differs from 170px

> **Tip:** `title_xpos="-100" title_ypos="-100"` hides window title text — Ruby Red does this on the main window because it uses a logo image instead.

> **.rgn files** define the window shape. Keep the ones from Ruby Red — they're interchangeable and rarely need changes.

### `<style>` vs `<override>`

Ruby Red uses `<style>` tags which **replace the entire Default style** — you must specify ALL attributes. Icy Blue uses `<override>` tags which **merge with Default** — simpler but less explicit. If starting from Ruby Red, stick with `<style>`.

---

## Step 5: Customize the Buddy List (FriendList.xml)

Open `FriendList/FriendList.xml` — this controls the buddy list layout. The key override is the `MePanel` which reserves space for character artwork:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<theme app="Y!Msgr" version="2">
  <section id="FriendList">
    <!-- Reserve 160px on the right of the Me panel for artwork -->
    <override id="MePanel" dock="top" resizemargin="2,59,160,1" />
  </section>
</theme>
```

Both Ruby Red and Icy Blue use this same override. Adjust the right value (`160`) if your artwork is wider or narrower.

### FriendList Image Assets

If you copied Ruby Red, replace these images in the `FriendList/` folder:

- **`me_bg.png`** (~169x61) — Character artwork on the right, solid/tileable color on the left
- **`SearchBar.png`**, **`SearchBar_h.png`**, **`SearchBar_fc.png`** — Search bar states (normal, hover, focused)
- **`btn-single-status.png`** — Status dropdown button
- **`PluginPanel.png`**, **`BottomPluginEdge.png`** — Plugin panel backgrounds

---

## Step 6: Customize the IM Window (IMWindow.xml)

Open `IMWindow/IMWindow.xml` — this controls the IM conversation window toolbar. Ruby Red's version:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<theme app="Y!Msgr" version="2">
  <section id="IMWindow">
    <!-- Remove 2px gap between menu bar and toolbar -->
    <override id="IMWnd.MainToolbarArea" margin="7,0,0,0" />

    <!-- Custom toolbar background with artwork on the right -->
    <override id="IMWnd.ToolbarArea"
        imagefile="toolbar_back.png"
        resizemargin="0,0,144,0"/>

    <!-- Status bar transparency (0=invisible, 255=fully opaque) -->
    <override id="IMWnd.StatusBarTag" alpha="69" />
    <override id="IMWnd.StatusBar" alpha="107" />
    <override id="IMWnd.StatusBarUrl" alpha="107" />
    <override id="IMWnd.StatusBarUrl2" alpha="107" />
  </section>
</theme>
```

### What to Modify

- **Replace `toolbar_back.png`** (~200x44px) — your character artwork on the right, tileable color on the left
- **Adjust `resizemargin` right value** (`144`) to match your artwork width
- **Adjust `alpha` values** — lower = more transparent (0 = invisible, 255 = fully opaque)

> Icy Blue uses a wider artwork area (`resizemargin="0,0,190,0"`) — adjust to fit your image.

---

## Step 7: Replace Image Assets

If you copied Ruby Red, all the image files are already in place — you just need to replace them with your own artwork. Here's every image Ruby Red includes, organized by folder:

### Root

| Image | Size | Purpose |
|---|---|---|
| `preview.png` | ~150x200 | Skin picker thumbnail |

### theme/

| Image | Size | Purpose |
|---|---|---|
| `mainframewindow.png` | ~190x128 | Buddy list window border |
| `framewindow.png` | ~190x192 | IM window border |
| `toolwindow.png` | ~97x74 | Popup window border |
| `Yahoo!_Messenger.png` | ~161x34 | Title bar logo |
| `ellipsis.png` | — | Title bar ellipsis |
| `menubar.png` | — | Menu bar item background |
| `menuitem.png` | — | Dropdown menu item background |
| `menu_bg.png` | — | Menu background |
| `headerbg.png` | — | List header background |
| `pushbuttons.png` | 50x132 | Button sprites (6 states stacked) |
| `tabs.png` | — | Tab control sprites |
| `grabber.png` | — | Grabber handle |
| `slotborder.png` | — | Plugin slot border |
| `slotborder_we_left.png` | — | Plugin slot left edge |
| `slotborder_we_right.png` | — | Plugin slot right edge |
| `scroll_vbg.png` | — | Vertical scrollbar background |
| `scroll_varrows.png` | — | Vertical scrollbar arrows |
| `scroll_v_grip.png` | — | Vertical scrollbar thumb |
| `scroll_hbg.png` | — | Horizontal scrollbar background |
| `scroll_harrows.png` | — | Horizontal scrollbar arrows |
| `scroll_h_grip.png` | — | Horizontal scrollbar thumb |
| `checkbox.bmp` | — | Custom checkbox sprite |
| `radio.bmp` | — | Custom radio button sprite |

### FriendList/

| Image | Size | Purpose |
|---|---|---|
| `me_bg.png` | ~169x61 | Me panel background |
| `SearchBar.png` | ~70x32 | Search bar (normal) |
| `SearchBar_h.png` | — | Search bar (hover) |
| `SearchBar_fc.png` | — | Search bar (focused) |
| `SearchBarButton.png` | — | Search bar button |
| `btn-single-status.png` | — | Status button |
| `DisplayImgOverlay.png` | — | Display image overlay |
| `AddBuddyPanel.png` | — | Add buddy panel background |
| `PluginPanel.png` | — | Plugin panel background |
| `PluginPanelFiller.png` | — | Plugin panel filler |
| `BottomPluginEdge.png` | — | Plugin panel bottom edge |

### IMWindow/

| Image | Size | Purpose |
|---|---|---|
| `toolbar_back.png` | ~200x44 | IM toolbar background |
| `im_tb_format.png` | — | Text format toolbar button |
| `im_tb_disp_img_toggle.png` | — | Display image toggle |

### images/

| Image | Size | Purpose |
|---|---|---|
| `bg_hover.png` | 1x(h) | List hover highlight (tiles horizontally) |
| `bg_selected.png` | 1x(h) | List selection highlight (tiles) |
| `btn-single-*.png` | — | Various button images |
| `resize_ctrl.png` | — | Window resize grip |

### ContactCard/

| Image | Purpose |
|---|---|
| `background.png` | Contact card background |
| `Frame.png` | Contact card frame |
| `CallButton.png` | Call button |
| `SmsButton.png` | SMS button |

> **Tip:** You don't have to replace every single image on day one. Start with the most visible ones (`mainframewindow.png`, `framewindow.png`, `me_bg.png`, `toolbar_back.png`, `preview.png`) and work through the rest. Images you don't replace will still use the Ruby Red versions.

> **Tip:** Images that tile (like `bg_hover.png`) can be just 1px wide — they'll repeat horizontally.

---

## Step 8: Install & Test

1. Copy your skin folder to the Yahoo! Messenger skins directory
2. Open Yahoo! Messenger → **Messenger** menu → **Change Skin**
3. Select your skin from the list

### Testing Checklist

- [ ] Buddy list background and text are readable
- [ ] Group headers have good contrast
- [ ] IM window text is legible
- [ ] Menus are readable (both menu bar and dropdowns)
- [ ] Buttons have visible text in all states
- [ ] Selection highlight is visible
- [ ] Window frames display correctly at different sizes
- [ ] Toolbar artwork doesn't stretch or tile oddly
- [ ] Contact card looks correct
- [ ] Scrollbars are visible and match your theme

---

## Quick-Start: Minimal Skin (Colors Only)

If you just want to change colors without any custom images, you only need **two files**:

```
My Color Skin/
├── colors.xml
└── Localized.xml
```

Copy these from Ruby Red (or any skin), change the colors, and you're done. Everything else falls back to Default.

---

## Tips & Common Pitfalls

- **resizemargin values must not exceed image dimensions** — this will crash the messenger.
- **Keep the stretch area small** (0–2px) and use solid colors in it to avoid tiling artifacts.
- **Test at different window sizes** — drag windows larger and smaller to catch stretch issues.
- **Dark theme?** Make sure `menuitemtext` stays dark (dropdown menus usually have a light background even in dark skins).
- **Invisible text?** Check that your text colors have enough contrast against the background. Dark-on-dark and light-on-light are common mistakes.
- **3px gap on the right edge?** Reduce `framewindow` resizemargin right from 5 to 2.
- **Gap between menu and toolbar?** Override `IMWnd.MainToolbarArea` margin top from 2 to 0.

---

## Further Reading

- [colors.xml](colors.xml) — Full color template with every ID documented
- [template-guide.md](template-guide.md) — Comprehensive reference for all skin components
- [windows-reference.md](windows-reference.md) — Reference for all skinnable windows
- [VOCALOID SKINS SET/](VOCALOID%20SKINS%20SET/) — Complete example skins to study
  - **Ruby Red - Teto** — Most complete skin, overrides nearly everything (best base for copying)
  - **Icy Blue - Hatsune Miku** — Simpler skin, fewer overrides (good for understanding basics)