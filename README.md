# MMBASIC.XML

This is a WORK IN PROGRESS<BR>

Many keywords are missing.<BR>


`MMBASIC.XML` is a **Notepad++ User Defined Language (UDL)** definition for **MMBasic** source files.

It is intended to improve the editing experience for MMBasic programs by adding syntax highlighting for common language elements used in `.bas` files.

## Features

- Highlights **MMBasic keywords**
- Highlights **built-in functions**
- Recognises **comments**
  - apostrophe comments: `'`
  - `REM` comments
- Highlights **strings**
- Highlights **numbers**
- Highlights **operators**
- Associates the language with **`.bas`** files

## Purpose

This file makes MMBasic source code easier to read and maintain in Notepad++ by applying language-aware colour highlighting to common BASIC constructs.

It is aimed at users writing or maintaining MMBasic programs on platforms such as:

- PicoMite
- Maximite
- Colour Maximite 2
- Armmite
- other MMBasic-compatible systems

## Scope

`MMBASIC.XML` is a **syntax-highlighting definition only**.

It does **not** provide:

- compilation
- linting
- debugging
- semantic parsing
- IntelliSense

For advanced features such as the Notepad++ **Function List** panel, a separate Function List parser XML may also be required.

## Installation

### Import through Notepad++

1. Open **Notepad++**
2. Go to **Language**
3. Select **User Defined Language**
4. Choose **Define your language...**
5. Click **Import**
6. Select `MMBASIC.XML`
7. Restart Notepad++ if required

### File association

After import, associate the UDL with:

```text
.bas
