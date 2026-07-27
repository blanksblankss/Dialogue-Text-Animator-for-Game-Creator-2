# Dialogue Text Animator for Game Creator 2

Bring expressive, animated dialogue text to **Game Creator 2 Dialogue** with a TextMeshPro-based workflow designed to fit naturally into GC2 projects.

[![Unity](https://img.shields.io/badge/Unity-6%2B-black?logo=unity)](https://unity.com/)
[![Game Creator 2](https://img.shields.io/badge/Game%20Creator%202-Dialogue-blue)](https://gamecreator.io/)
[![TextMeshPro](https://img.shields.io/badge/TextMeshPro-Required-orange)](https://docs.unity3d.com/Packages/com.unity.textmeshpro@latest)
[![Asset Store](https://img.shields.io/badge/Unity%20Asset%20Store-View%20Asset-000000?logo=unity)](https://assetstore.unity.com/packages/tools/utilities/dialogue-text-animator-for-game-creator-2-370116)

> **Dialogue Text Animator for Game Creator 2** adds per-tag text animation, styling, typewriter effects, optional audio, editor-assisted tagging, and GC2 visual-scripting hooks to Dialogue Speech UI without modifying the official Game Creator 2 packages.

## Get the Asset

**Unity Asset Store:**  
https://assetstore.unity.com/packages/tools/utilities/dialogue-text-animator-for-game-creator-2-370116

This repository provides public documentation and setup information for the Asset Store package. The package itself is distributed through the Unity Asset Store.

---

## Features

- **TextMeshPro-based dialogue animation** for Game Creator 2 Dialogue Speech UI
- **Per-tag animation and styling** using TMP link tags such as `dta:joy`, `dta:fear`, or your own tag IDs
- **Tag Style Packs** for reusable dialogue styles
- **Animation Profiles** and **Style Profiles** for reusable configuration
- **Optional typewriter audio** through Typewriter Audio Profiles
- **Tagging Assistant** for selecting text and applying tags without manually writing markup
- **Nested tags** for combining effects inside the same word or phrase
- **Stable typewriter reveal** designed to avoid disruptive layout movement
- **Skip / complete reveal support**
- **Message-bubble-safe layout reveal**
- **Game Creator-compatible visual scripting** for reveal control, state checks, properties, and events
- **Runtime + Editor integration** without editing Game Creator 2 source files

---

## Requirements

| Requirement | Notes |
| --- | --- |
| **Unity** | Unity 6+ |
| **Game Creator 2 Core** | Required |
| **Game Creator 2 Dialogue** | Required |
| **TextMeshPro** | TMP Essentials must be imported |
| **UGUI** | Required |

> **Recommended:** Create a prefab variant of your GC2 Speech UI and add `DialogueTextAnimator` only to your custom variant. This keeps the official Game Creator 2 Dialogue UI untouched.

---

## Quick Start

### 1. Create or use a GC2 Speech UI prefab variant

Create a prefab variant from the Speech UI used by **Game Creator 2 Dialogue**.

Keeping your integration in a variant makes upgrades safer and avoids modifying the official Dialogue UI prefab.

### 2. Find the dialogue TextMeshPro object

Inside the Speech UI prefab, locate the `TextMeshProUGUI` / `TMP_Text` object used for the spoken dialogue message.

### 3. Add `DialogueTextAnimator`

Add the component to the **same GameObject** as the TMP dialogue text component:

```text
DialogueTextAnimator
```

### 4. Assign profiles

In the `DialogueTextAnimator` inspector, assign or create:

- **Animation Profile**
- **Style Profile**
- **Typewriter Audio Profile** — optional
- **Tag Style Pack** — optional, but recommended

The default Tag Style Pack is a good starting point.

### 5. Tag dialogue text

The animator uses TextMeshPro link tags with a `dta:` identifier:

```html
This is <link="dta:fear">dangerous</link>.
```

At runtime, `dta:fear` is resolved through the assigned Tag Style Pack or local overrides.

Paste the final tagged text into your normal **Game Creator 2 Dialogue** node. GC2 continues to process the speech normally while `DialogueTextAnimator` reads the TMP tags and applies the configured animation and styling.

---

## Tagging Assistant

The included **Tagging Assistant** makes tagged dialogue easier to author.

Typical workflow:

1. Paste or type dialogue into the **Dialogue Text** field.
2. Select a word or phrase.
3. Click a style in the **Tagged Styles** panel.
4. The selected text is wrapped automatically.

Example:

```html
<link="dta:joy">workflow</link>
```

### Nested Tags

Nested tags are supported:

```html
<link="dta:joy">w<link="dta:glitch">o</link>rk<link="dta:threatening">flow</link></link>
```

Tagged fragments in the Preview can be clicked to jump back to their matching source range, making it easier to edit complex dialogue styling.

---

## Game Creator 2 Visual Scripting

The package includes Game Creator-compatible visual-scripting entries for integrating animated dialogue with gameplay logic, including:

- reveal-control **Instructions**
- reveal-state **Conditions**
- reveal progress and tag-state **Properties**
- **Events** for tag visibility and reveal moments

This allows gameplay logic to respond to dialogue animation and to specific tagged-word reveal states.

---

## Runtime Behavior

`DialogueTextAnimator` connects to the active GC2 `SpeechUI` behavior and does **not** require modifications to the official Game Creator 2 Dialogue source.

Runtime support includes:

- stable typewriter reveal
- per-tag style lookup
- optional typewriter audio
- skip / complete reveal
- message-bubble-safe layout reveal

> For message-bubble UI, keep **Stable Typewriter Layout** enabled unless your custom UI specifically requires different layout behavior.

---

## Documentation

For the complete setup workflow, Tagging Assistant usage, editing notes, and troubleshooting, see:

**[Quick Setup Guide](docs/quick-setup.md)**

---

## Example

Source dialogue:

```html
What changed <link="dta:secret">after the ritual</link>?
```

The text remains valid Game Creator 2 Dialogue content. At runtime, the animator detects the `dta:secret` link and applies the style/animation configured for that tag.

---

## Troubleshooting

### Tags appear as plain text

Check that:

- `DialogueTextAnimator` is on the TMP dialogue text object
- Game Creator 2 is using the Speech UI prefab variant containing the animator
- the tag exists in the assigned Tag Style Pack or local overrides
- the tag uses the expected format:

```html
<link="dta:tag-id">Text</link>
```

### No animation plays

Check that:

- an Animation Profile is assigned
- the dialogue text object is a TMP component
- the active Dialogue UI is using the prefab containing `DialogueTextAnimator`
- the package assemblies compile without errors

### Text selection looks incorrect in the Tagging Assistant

The source Dialogue Text field intentionally uses **no word wrap** because wrapped multiline UI Toolkit text can produce visually inaccurate native text selection.

Use the horizontal scrollbar for long source lines and the Preview panel for readable wrapped text.

---

## About

Developed by **Indie Blankz** for projects using **Game Creator 2 Dialogue** and TextMeshPro.

The goal is to add expressive dialogue presentation while keeping the GC2 workflow intact and the official Game Creator packages untouched.

---

> Build systems that respect the player,  
> tools that respect the developer,  
> and scope that respects reality.
