# dotfiles (archive)
This is the archive branch of my dotfiles repo.

<table>
	<tr>
		<td>
<!-- AUTO-GENERATED-CONTENT:START (TOC:collapse=true&collapseText=Table of Contents) -->
<details>
<summary>Table of Contents</summary>

- [Abricotine](#abricotine)
- [Atom](#atom)
- [Vivaldi](#vivaldi)
- [zsh](#zsh)

</details>
<!-- AUTO-GENERATED-CONTENT:END -->
		</td>
	</tr>
</table>


## [Abricotine](abricotine)
*Symlinked as ~/.config/Abricotine/app*

Markdown editor with custom theme support. No transparency out of the box but could probably be modified in the same way as Atom, though I like it better opaque. My wal theme is based on the default dark theme. I haven't figured out how to make it refresh the theme automatically yet so it must be done manually (ctrl+F5).

## [Atom](atom)
*Symlinked as ~/.atom*

Because it does not support transparent themes out of the box (on Linux, at least), I needed to make a quick modification to its internals. Don't worry, it doesn't involve building anything from source. Here are the steps I followed:
0. Make sure you have `npm`, then install `asar` with `sudo npm i -g asar`.
1. Exit Atom completely.
2. cd into `/usr/share/atom/resources/`, then unpack the main program with `sudo asar extract app.asar app.asar.extracted`. You must use `sudo` because it's in a write-protected directory.
3. Open the file `app.asar.extracted/src/main-process/atom-window.js` in your text editor of choice (with root privileges).
4. Around line 38 inside the `options` object and outside of the `webPreferences` object, add the line `transparent: true,` which will make the window background transparent. (I've also added `frame: false,` to mine which will hide the window title and menu bars. You don't have to.)
5. Save this file, then package it back up in the terminal with `sudo asar pack app.asar.extracted app.asar`. If you did it correctly you should be able to start Atom again! You won't see a difference at first because...
6. You need a theme that supports transparency! I'm using my [Fang](https://github.com/katacarbix/fang-ui) and [Wave](https://github.com/katacarbix/wave-ui) UI themes (dark and light mode, respectively). [native-ui](https://atom.io/themes/native-ui) works rather well too.

I wrote some styles to go along with Fang/Wave in [my stylesheet](atom/styles.less) that adds colors from pywal.

## Vivaldi
Vivaldi can use [custom CSS](vivaldi/common.css) with an [experimental toggle](https://forum.vivaldi.net/topic/37802/css-modifications-experimental-feature) which is nice, but it doesn't go so far as to be pywal-friendly without having to restart every time. Fortunately I can use [this script](scripts/vivwal) (by [wismut on vivaldi.net](https://forum.vivaldi.net/topic/34521/linux-changing-theme-via-command-line/22?_=1597433612704) and slightly modified by me) to set the theme colors through a remote Chromium console. It's pretty clever honestly. Vivaldi must be started with the command `vivaldi --remote-debugging-port=9222` for this to work.

## [zsh](misc/.zshrc)
Nothing special. Uses oh my zsh.
