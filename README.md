# Bim - A Bad IMitation of Vi(m)

![screenshot](screenshot.png)

Bim is a terminal text editor with syntax highlighting.

Inspired by Vim and featuring similar mode-based editing, Bim was originally written for ToaruOS, but it has also been tested in Linux, Sortix, FreeBSD, and macOS.

## Goals / Purpose

Bim does not seek to improve or replace vim, or any other text editor. Its goal is to provide ToaruOS-NIH - a hobby operating system built completely from scratch - with a featureful editor. The ability to build and run Bim on other platforms is a secondary feature.

## Features

- Vim-like modal interactions.
- Arrow-key and traditional vi hjkl navigation.
- Syntax highlighting (currently for C, Python, and Makefiles).
- Themes, including 256-color and 24-bit color support.
- Indentation adjustment.
- Multiple editor tabs.
- Basic Unicode support (sufficient for things like Japanese, but not capable of more complex scripts).
- Efficient screen redrawing.
- Terminal support tested in ToaruOS, Sortix, xterm, urxvt, Gnome, XFCE, Linux and FreeBSD consoles, macOS Terminal.app, iTerm2.
- Mouse support in Xterm-like terminals.
- Line selection and yanking.
- Incremental forward search (and backwards find-next).
- Undo/redo stack (experimental, enable with `-O history`)

## Prerequisites

Bim has no external dependencies beyond a functioning C library and sufficient escape code support in the hosting terminal.

### Terminal Support

Unicode support is recommended, but not completely required.

256-color and 24-bit color are optional. The default theme uses only the standard 16 colors.

Scrolling is normally done through `^[[1S` and `^[[1T`, but this can be disabled with the `:noscroll` command.

Mouse support with `^[[?1000h` is available. The alternate screen is used if available with `^[[?1049h`.

## Key Bindings

In normal, INSERT, LINE SELECTION, and REPLACE modes:

| **Key**    | **Action**                                      |
|------------|-------------------------------------------------|
| Arrows     | Move the cursor                                 |
| Page Up    | Scroll up one screenful                         |
| Page Down  | Scroll down one screenful                       |
| Home       | Move cursor to start of line                    |
| End        | Move cursor to end of line (past end in INSERT) |
| Ctrl-Left  | Move to start of previous word                  |
| Ctrl-Right | Move to start of next word                      |
| Escape     | Return to normal mode                           |

When in normal mode:

| **Key**     | **Action**                                                                              |
|-------------|-----------------------------------------------------------------------------------------|
| `:`         | Start entering a command                                                                |
| `/`         | Start incremental search                                                                |
| `n`         | Find next search match                                                                  |
| `N`         | Find previous search match                                                              |
| `V`         | Enter LINE SELECTION mode                                                               |
| `R`         | Enter REPLACE mode                                                                      |
| `i`         | Enter INSERT mode                                                                       |
| `a`         | Enter INSERT mode with the cursor after the current position (for appending characters) |
| `O`         | Add line before current line, and enter INSERT mode.                                    |
| `o`         | Add line after current line, and enter INSERT mode.                                     |
| `hjkl`      | Vi-style navigation                                                                     |
| Space       | Scroll down a screenful                                                                 |
| `%`         | Jump to the matching brace/parenthesis                                                  |
| `{`         | Jump to previous blank line                                                             |
| `}`         | Jump to next blank line                                                                 |
| `$`         | Move the cursor to the end of the line                                                  |
| `^` or `0`  | Move the cursor to the beginning of the line                                            |
| `Pp`        | Paste yanked lines, before or after (respectively)                                      |
| `u`         | Undo last block of edits                                                                |
| Ctrl-`R`    | Redo last undone block of edits                                                         |
| Ctrl-`L`    | Repaint the screen                                                                      |

In LINE SELECTION mode the following additional commands are available:

| **Key**     | **Action**                                               |
|-------------|----------------------------------------------------------|
| Tab         | Indent selected lines one indentation unit to the right  |
| Shift-Tab   | Unindent selected lines one indentation unit to the left |
| `d`         | Delete and yank selected lines                           |
| `y`         | Yank selected lines                                      |

## Commands

| **Command**        | **Description**                                                                                |
|--------------------|------------------------------------------------------------------------------------------------|
| `:e FILE`          | Open `FILE` in a new tab                                                                       |
| `:tabnew`          | Create a new empty tab                                                                         |
| `:w`               | Write the current file                                                                         |
| `:w FILE`          | Write the current buffer to `FILE`                                                             |
| `:wq`              | Write the current file and close this buffer                                                   |
| `:q`               | Close this buffer if it has not been modified                                                  |
| `:q!`              | Close this buffer even if it has been modified                                                 |
| `:qa`              | Try to close all buffers                                                                       |
| `:qa!`             | Quit immediately, ignoring unsaved changes                                                     |
| `:tabp`            | Switch to previous tab                                                                         |
| `:tabn`            | Switch to next tab                                                                             |
| `:indent`          | Enable automatic indentation                                                                   |
| `:noindent`        | Disable automatic indentation                                                                  |
| `:noh`             | Clear search string                                                                            |
| `:theme`           | Print the current selected color scheme                                                        |
| `:theme THEME`     | Set the color scheme to `THEME` (use tab completion to see available themes)                   |
| `:noscroll`        | Disable the use of special terminal escapes when scrolling.                                    |
| `:syntax`          | Print the current syntax highlighting mode (also displayed in the status bar)                  |
| `:syntax LANGUAGE` | Set the syntax highlighting mode to `LANGUAGE` (use tab completion to see available languages) |
| `:recalc`          | Recalculate syntax highlighting for the whole buffer                                           |
| `:tabs`            | Set the tab key and automatic indentation to insert tab characters                             |
| `:spaces`          | Set the tab key and automatic indentation to insert spaces                                     |
| `:tabstop`         | Print the current tab stop (how wide one indentation unit is)                                  |
| `:tabstop TABSTOP` | Set the tab stop width                                                                         |
| `:clearyank`       | Clear the yank buffer                                                                          |

## Additional Bim Functionality

You can use Bim to display files in your terminal with syntax higlighting with `bim -c` (no line numbers) and `bim -C` (with line numbers).

![screenshot](screenshot_cat.png)

You can pipe text to bim for editing with `bim -`. Note that Bim will wait for end-of-file before launching, so this is not suitable for use as a pager (pager support is planned).

## License

Bim is primarily distributed under the ISC license. In ToaruOS, it is under the NCSA license. The terms are nearly identical from a legal standpoint.

## Development

Bim is still primarily developed alongside ToaruOS-NIH. This repository is a mirror with fake history going back to the start of that project. Pull requests merged here will be patched into [ToaruOS-NIH](https://git.toaruos.org/klange/toaru-nih).
