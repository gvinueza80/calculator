# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Running

Open `index.html` directly in a browser — no build step, no server, no dependencies.

## Architecture

Single file: `index.html`. All markup, styles, and logic inline.

**Display model:** two lines — top (`#expr`) shows the full expression being built; bottom (`#curr`) shows current input or result.

**State machine** (all state in one `state` object):
- `cur` — string shown on bottom line
- `expr` — string shown on top line
- `lop` — left operand for the pending binary operation
- `op` — pending operator (`+`, `-`, `*`, `/`)
- `wait` — true immediately after pressing an operator; next digit starts a fresh `cur`
- `done` — true after `=` or a unary op; next digit starts a fresh expression

**Operators:** `+`, `−`, `×`, `÷` (binary); `√`, `1/x` (unary, act on `cur`, set `done=true`); `+/−` (negate `cur`); `%` (percent — `X% of lop` for `+`/`−` context, else `X/100`).

**Error state:** `cur = 'Error'`, all other state cleared. Triggers on: division by zero, `√` of negative, non-finite result. Clears on next digit input.

**Keyboard:** `0–9`, `.`, `+`, `-`, `*`, `/` (preventDefault), `Enter`/`=`, `Backspace`, `Escape`, `%`.

**Number formatting:** `parseFloat(n.toPrecision(10))` removes floating-point noise; falls back to 6 sig-figs if result string exceeds 13 chars.
