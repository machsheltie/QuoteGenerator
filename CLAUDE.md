# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Is

A single-file standalone React quote generator (`quote_generator.jsx`) for Aaron's Lawn Care. No build system, no package.json — it's a self-contained component designed to be dropped into a host app or run in a sandbox (e.g., CodeSandbox, StackBlitz).

## Architecture

The entire app lives in one file with two components:

**`PrintableQuote`** (line 45) — A read-only, print-optimized layout rendered when the user clicks Print/Save PDF. Receives `quoteData` and `items` as props. Styled with inline styles and targets `@media print` via a `<style>` tag injected into the DOM at print time.

**`QuoteGenerator`** (line 305, default export) — The interactive form. Manages all state locally with `useState`:
- `customerName`, `customerAddress`, `quoteDate`, `quoteNumber`, `notes` — quote header fields
- `items` — array of `{ description, qty, unitPrice }` line items
- `showPreview` — toggles between form view and print preview

Key handlers:
- `handlePrint` — injects print styles and calls `window.print()`
- `handleNew` — resets all state for a new quote
- `addItem` / `removeItem` / `updateItem` — manage the line items array

## Styling

All styles are inline objects defined at the top of `QuoteGenerator` (`inputStyle`, `labelStyle`, `btnPrimary`, `btnSecondary`). The `BRAND` constant (line 3) holds the full color palette. No Tailwind or CSS files.

## Logo

`LOGO_SRC` (line 17) is a base64-encoded PNG embedded directly in the file — no external image dependency.

## Usage

To embed in another React app:

```jsx
import QuoteGenerator from './quote_generator';

function App() {
  return <QuoteGenerator />;
}
```

Requires only `react` and `react-dom`. No other dependencies.
