# AI Handoff Notes

This document is for future AI assistants or developers maintaining this project.

Project name:

```txt
小动物画画监督日历
```

Repository:

```txt
drawing-recovery-calendar
```

GitHub Pages:

```txt
https://kirpearlzayneowo-afk.github.io/drawing-recovery-calendar/
```

Current recommended open-source version:

```txt
v4.2
```

## Project Purpose

This is a local-first drawing recovery check-in calendar.

It is not designed to measure productivity.

It is designed to help the user gently return to drawing.

Core principle:

> Opening the drawing software counts as a valid start.

The tool should reduce pressure, not increase it.

## Current Version

Current UI footer:

```txt
Version v4.2 · local-first
```

Current localStorage key:

```js
animalDrawingCalendar.v4_2
```

Old versions are read for migration:

```js
animalDrawingCalendar.v4_1
animalDrawingCalendar.v4
animalDrawingCalendar.v3
foxDrawingCalendar.v2
foxDrawingCalendar.v1
```

## v4.2 Core Changes

- Default theme changed to `樱花猫猫`.
- The open-source default experience is light, soft, and public-friendly.
- Original `莓果夜` was renamed / adjusted to `星莓夜`.
- Guardians now support custom:
  - `icon`
  - `name`
  - `mark`
  - `doneText`
- Calendar completion mark is no longer fixed as `🐾`.
- Completion text is no longer fixed as “盖爪印”.
- Non-paw guardians can use more suitable marks and done messages.
- Example:
  - `mark: "🫧"`
  - `doneText: "小鱼吐了一个泡泡。"`
- Added optional “给 Char 的小礼物” module.
- Added custom work types.
- Added custom completion levels.
- Added visible version footer.

## Data Structures

### Animal

```ts
type Animal = {
  icon: string;
  name: string;
  mark: string;
  doneText: string;
};
```

Example:

```js
{
  icon: "🐟",
  name: "小鱼",
  mark: "🫧",
  doneText: "小鱼吐了一个泡泡。"
}
```

### DayEntry

```ts
type DayEntry = {
  level: number;
  types: string[];
  customWork: string;
  mood: string;
  gift: string;
  customGift: string;
  reward: string;
  note: string;
  updatedAt: string;
};
```

### Settings

```ts
type Settings = {
  userName: string;
  charName: string;
  theme: string;
  animalIcon: string;
  animals: Animal[];
  levels: Level[];
  workTypes: string[];
  moods: string[];
};
```

### Level

```ts
type Level = {
  value: number;
  label: string;
  done: boolean;
};
```

## About “给 Char 的小礼物”

“给 Char 的小礼物” is not a streak repair feature.

It is not:

- make-up check-in
- debt
- punishment
- penalty
- productivity pressure

Its product purpose is:

> If the user missed a day, or wants to gently return to drawing, they may choose a small optional practice as a gift.

The low-pressure option must remain:

```txt
今天不需要
```

Do not ask the user to explain why they do not need a gift today.

Sometimes restarting does not need a reason.

## About Page Title / Subtitle Customization

v4.1 tried exposing page title and subtitle customization in the UI.

This made the top section feel too heavy and increased configuration pressure before the user could start checking in.

v4.2 removed this UI.

If a user wants to personalize the page title or subtitle, modify `index.html` directly.

Title location:

```html
<h1>小动物画画监督日历</h1>
```

Subtitle logic location:

```js
$("subtitle").textContent = "今日监督员：" + a.name + "。打开绘画软件就算一次有效开始。";
```

Do not expose this as default UI unless the user explicitly asks for it.

## About Reset / Restore Defaults

v4.2 does not include a “restore defaults” button.

Reason:

- It may accidentally delete user-customized guardians, levels, work types, or moods.
- It is risky for non-technical users.
- JSON backup / import already exists.

If a future version adds reset functionality, it must:

1. Ask the user explicitly.
2. Use a second confirmation.
3. Preferably export a backup before deleting anything.
4. Clearly distinguish between:
   - clearing one day
   - clearing all data
   - restoring default settings

## Product Principles

1. Do not upload user data by default.
2. Preserve the local-first principle.
3. “只是打开” must count as completion.
4. Do not design missed days as failure.
5. Do not turn “给 Char 的小礼物” into punishment.
6. Users do not need to justify choosing “今天不需要”.
7. Keep the UI lightweight.
8. Do not expose low-frequency settings on the first screen unless necessary.
9. Prefer emotional safety over feature completeness.
10. The tool should make returning to drawing easier, not heavier.

## Open Source Safety Notes

The open-source version should remain public-friendly.

Do not add relationship-specific defaults such as:

```txt
猫猫 / 老公
```

The default names should remain:

```txt
User / Char
```

Users can personalize these locally through the UI.

## Maintenance Notes

This is currently a single-file frontend project.

Main file:

```txt
index.html
```

No build step is required.

No backend is required.

No database is required.

Data is stored in browser `localStorage`.

If future changes introduce external services, syncing, accounts, or cloud storage, update this document and the README privacy section.