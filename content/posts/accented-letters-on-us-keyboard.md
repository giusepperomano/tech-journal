---
Title: Typing Accented Letters on a Keyboard with US Layout
date: 2021-12-05
tags:
- linux
- internationalization
---
## Introduction

This note explains how to type accented characters on a US/layout keyboard
in Ubuntu Linux using the **Compose key**.

## Configuration

Configure **Right Alt** as the compose key from GNOME settings:

! compose key configuration](/images/configure-compose-key-in-gnome.png)

Alternatively you can enable it from the command line:

```bash
gsettings set org.gnome.desktop.input-sources xkb-options " 'compose:ralt']
```

## Key Sequences

|Character|Sequence|
|:---:|---|
|é|**Right Alt** + ‘ + e|
|è|**Right Alt** + ` + e|
|ü|**Right Alt** + “ + u|
|ô|**Right Alt** + ^ + o|
|ç|**Right Alt** + , + c|
|ñ|**Right Alt** + ~ + n|
|å|**Right Alt** + o + a|
|æ|**Right Alt** + a + e|
|Œ|**Right Alt** + O + E|
|ø|**Right Alt** + / + o|
|ß|**Right Alt** + s + s|
|€|**Right Alt** + e + =|

## Links

[How can I type accented characters like ë?](https://askubuntu.com/questions/358/how-can-i-type-accented-characters-like-%C3%AB)
