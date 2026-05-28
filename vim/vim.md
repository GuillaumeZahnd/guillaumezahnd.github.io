---
layout: default
title: Vim
nav_order: 3
parent: Foundations
grand_parent: Home
has_children: false
---

# Vim

## General

| Command | Effect |
| --- | --- |
| r\<c> | Replace the character under the cursor with character \<c> |
| gUiw | Convert each character in the current word to uppercase |
| guiw | Convert each character in the current word to lowercase |
| ciw | Replace inner word |
| gg=G | Automatically indent file |
| d0 | Delete text from start of line to cursor |
| D | Delete text from cursor to end of line |
| 0D | Delete entire line (except linebreak) |


## Buffer

| Command | Effect |
| --- | --- |
| :ls | Show the list of current buffers |
| :e <path and file> | Open a new file in buffer (Add `set wildmenu` in `.vimrc` for enhanced tab completion) |
| :b \<filename> | Switch to \<filename> in buffer |
| :b# | Quickly switch to the last visited file in buffer |
| :bp | Switch to the previous file in buffer |
| :bn | Switch to the next file in buffer |
| :b\<n> | Switch to the n-th file in buffer |
| :bd <filename> | Delete \<filename> from buffer |
| :mksession! ~/\<session name>.ses | Save current session |
| vim -S ~/\<session name>.ses | Load session |

