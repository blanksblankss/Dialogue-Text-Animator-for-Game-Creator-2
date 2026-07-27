# Dialogue Text Animator for Game Creator 2 — Quick Setup Guide

**Version:** 0.6.161  
**Target:** Unity 6+

## Overview

| | |
| --- | --- |
| **Depends on** | Game Creator 2 Core, Game Creator 2 Dialogue, TextMeshPro, UGUI |
| **Affects** | Runtime and Editor |
| **Purpose** | Adds TextMeshPro-based dialogue text animation to GC2 Dialogue Speech UI |

> **Recommended:** Use a prefab variant of your GC2 Speech UI and add `DialogueTextAnimator` only to your custom prefab variant.

This guide covers the minimum setup needed to install and use the module with Game Creator 2 Dialogue. The module extends GC2 Dialogue through custom Runtime and Editor code; the official Game Creator 2 packages remain untouched.

---

## 1. Import Requirements

Before importing this module, make sure the project already has:

- Game Creator 2 Core
- Game Creator 2 Dialogue
- TextMeshPro Essentials imported
- UGUI available in the project

Import this module under your custom asset folder, for example:

```text
Assets/Indie Blankz/Dialogue Text Animator for Game Creator 2
```

---

## 2. Recommended Setup Flow

### Step 1 — Use or create a GC2 Speech UI prefab variant

Use a prefab variant of your Game Creator 2 Dialogue Speech UI. This keeps the official Dialogue UI prefab untouched.

Recommended location example:

```text
Assets/Indie Blankz/Dialogue Text Animator for Game Creator 2/Prefabs
```

### Step 2 — Select the TextMeshPro text object

Inside the Speech UI prefab, find the TMP text object used for the spoken dialogue message.

It is usually the text object controlled by GC2 Dialogue's `SpeechUI` component.

### Step 3 — Add `DialogueTextAnimator`

Add this component to the TMP dialogue text object:

```text
DialogueTextAnimator
```

The component should be on the same GameObject as the `TMP_Text` / `TextMeshProUGUI` component.

### Step 4 — Assign profiles

In the `DialogueTextAnimator` inspector, assign or create:

- **Animation Profile**
- **Style Profile**
- **Typewriter Audio Profile** — optional
- **Tag Style Pack** — optional, but recommended

The default Tag Style Pack can be used as a starting point.

---

## 3. Tagging Assistant Workflow

Open the **Tagging Assistant** from the module menu or from the `DialogueTextAnimator` inspector tools.

The Tagging Assistant wraps selected dialogue text with `dta:` link tags.

Example source text:

```html
This is <link="dta:fear">dangerous</link>.
```

The tag ID is:

```text
dta:fear
```

At runtime, the module resolves that tag through the assigned Tag Style Pack or local overrides.

---

## 4. Using the Tagging Assistant

### Basic tagging

1. Paste or type dialogue text into the **Dialogue Text** field.
2. Select a word or phrase in the Dialogue Text field.
3. Click a style in the **Tagged Styles** panel.
4. The selected range is wrapped automatically.

Example result:

```html
<link="dta:joy">workflow</link>
```

### Preview click-to-select

- Click a tagged Preview fragment to select its matching source range in the Dialogue Text field.
- The Dialogue Text field scrolls horizontally to the selected source range if needed.
- Then click another style in Tagged Styles to re-wrap or nest styling as needed.

### Nested tags

Nested tags are supported.

Example:

```html
<link="dta:joy">w<link="dta:glitch">o</link>rk<link="dta:threatening">flow</link></link>
```

Inner tagged fragments are clickable separately in the Preview.

---

## 5. Dialogue Text Field Behavior

The Dialogue Text input is intentionally kept in **no-wrap** mode.

This is important because Unity UI Toolkit multiline text selection can become visually inaccurate when word wrap is enabled. No-wrap mode keeps native selection accurate.

Long lines use a horizontal scrollbar instead.

### Recommended editing workflow

- Use the **Dialogue Text** field for accurate source selection.
- Use the **Preview** panel for readable wrapped preview.
- Click Preview tags to jump back to the matching source text.

---

## 6. Applying the Text to Game Creator Dialogue

After tagging text, copy the final source text from the Dialogue Text field and paste it into your Game Creator 2 Dialogue node text.

Example:

```html
What changed <link="dta:secret">after the ritual</link>?
```

At runtime, the dialogue text is still processed by GC2 Dialogue, while `DialogueTextAnimator` reads the TMP link tags and applies visual animation and styling.

---

## 7. Runtime Notes

The module is designed to work with Game Creator 2 Dialogue Speech UI by connecting to the active `SpeechUI` behavior.

It does not require editing the official GC2 Dialogue source.

Runtime behavior includes:

- stable typewriter reveal
- per-tag style lookup
- optional typewriter audio
- skip / complete reveal support
- message-bubble-safe layout reveal

> **Message bubble UI:** Keep **Stable Typewriter Layout** enabled unless you have a custom layout reason to disable it.

---

## 8. Visual Scripting Support

The module includes Game Creator-compatible visual scripting entries such as:

- instructions for reveal control
- conditions for reveal state
- properties for reveal progress and tag state
- events for tag visibility / reveal moments

Use these when gameplay needs to react to dialogue text animation or tagged-word reveal states.

---

## 9. Common Troubleshooting

### Selection looks wrong when editing text

Keep Dialogue Text input wrapping off. The module is configured this way by default.

Use the Preview panel for wrapped readability instead.

### Preview click selects the correct source text, but I cannot see it

Use the Dialogue Text horizontal scrollbar.

Preview click-to-select also attempts to scroll the source field to the tagged range automatically.

### Tags appear as plain text during runtime

Check that:

- `DialogueTextAnimator` is on the TMP dialogue text object
- the Speech UI prefab variant is the one used by GC2 Dialogue
- the tag style exists in the assigned Tag Style Pack
- the tag format uses `link="dta:tag-id"`

Example:

```html
<link="dta:fear">dangerous</link>
```

### No animation plays

Check that:

- an Animation Profile is assigned
- the text object is a TMP text component
- the active Dialogue UI is using the prefab with `DialogueTextAnimator`
- the module assemblies compile without errors

---

## Asset Store

[Dialogue Text Animator for Game Creator 2 on the Unity Asset Store](https://assetstore.unity.com/packages/tools/utilities/dialogue-text-animator-for-game-creator-2-370116)
