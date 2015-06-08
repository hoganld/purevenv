# Pure VENV

> ZSH prompt based on the excellent "Pure" by Sindre Sorhus, adding Python Virtualenv information to the prompt

![](screenshot.png)


## Overview

Most prompts are cluttered, ugly and slow. I wanted something visually pleasing that stayed out of my way.

### Why?

- Comes with the perfect prompt character.  
  Author went through the whole Unicode range to find it.
- Shows `git` branch and whether it's dirty (with a `*`).
- Indicates when you have unpushed/unpulled `git` commits with up/down arrows.
- Prompt character turns red if the last command didn't exit with `0`.
- Command execution time will be displayed if it exceeds the set threshold.
- Username and host only displayed when in an SSH session.
- Shows the current path in the title and the [current folder & command](screenshot-title-cmd.png) when a process is running.
- Makes an excellent starting point for your own custom prompt.


## Install

Must be installed manually. Requires git 2.0.0+ and ZSH 5.0.0+.

1. Either…
  - Clone this repo
  - add it as a submodule, or
  - just download `purevenv.zsh`

2. Symlink `kitanai.zsh` to somewhere in [`$fpath`](http://www.refining-linux.org/archives/46/ZSH-Gem-12-Autoloading-functions/) with the name `prompt_purevenv_setup`.

3. Symlink `async.zsh` in `$fpath` with the name `async`.

#### Example

```
$ ln -s "$PWD/purevenv.zsh" /usr/local/share/zsh/site-functions/prompt_purevenv_setup
$ ln -s "$PWD/async.zsh" /usr/local/share/zsh/site-functions/async
```
*Run `echo $fpath` to see possible locations.*

For a user-specific installation (which would not require escalated privileges), simply add a directory to `$fpath` for that user:

```sh
# .zshenv or .zshrc
fpath=( "$HOME/.zfunctions" $fpath )
```

Then install the theme there:

```sh
$ ln -s "$PWD/purevenv.zsh" "$HOME/.zfunctions/prompt_purevenv_setup"
$ ln -s "$PWD/async.zsh" "$HOME/.zfunctions/async"
```


## Getting started

Initialize the prompt system (if not so already) and choose `purevenv`:

```sh
# .zshrc
autoload -U promptinit && promptinit
prompt purevenv
```


## Options

### `PUREVENV_CMD_MAX_EXEC_TIME`

The max execution time of a process before its run time is shown when it exits. Defaults to `5` seconds.

### `PUREVENV_GIT_PULL`

Set `PUREVENV_GIT_PULL=0` to prevent Purevenv from checking whether the current Git remote has been updated.

### `PUREVENV_GIT_UNTRACKED_DIRTY`

Set `PUREVENV_GIT_UNTRACKED_DIRTY=0` to not include untracked files in dirtiness check. Only really useful on extremely huge repos like the WebKit repo.

### `PUREVENV_GIT_DELAY_DIRTY_CHECK`

Time in seconds to delay git dirty checking for large repositories (git status takes > 2 seconds). The check is performed asynchronously, this is to save CPU. Defaults to `1800` seconds.

### `PUREVENV_PROMPT_SYMBOL`

Defines the prompt symbol. The default value is `❯`.

## Example

```sh
# .zshrc

autoload -U promptinit && promptinit

# optionally define some options
PUREVENV_CMD_MAX_EXEC_TIME=10

prompt purevenv
```


## Tips

[Tomorrow Night Eighties](https://github.com/chriskempson/tomorrow-theme) theme with the [Droid Sans Mono](http://www.google.com/webfonts/specimen/Droid+Sans+Mono) font (15pt) is a beautiful combination, as seen in the screenshot above. Just make sure you have anti-aliasing enabled in your Terminal.

To have commands colorized as seen in the screenshot install [zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting).


## ZSH Framework Integration

### [oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh)

Symlink (or copy) `purevenv.zsh` to `~/.oh-my-zsh/custom/purevenv.zsh-theme` and add `ZSH_THEME="purevenv"` to your `.zshrc` file.

### [prezto](https://github.com/sorin-ionescu/prezto)

Set `zstyle ':prezto:module:prompt' theme 'purevenv'` in `~/.zpreztorc`.

### [antigen](https://github.com/zsh-users/antigen)

Add `antigen bundle sindresorhus/purevenv` to your .zshrc file (do not use the `antigen theme` function).

## Virtualenvwrapper Integration

Symlink (or copy) `postactivate` to your $WORKON directory.

For details, see the [Virtualenvwrapper docs](http://virtualenvwrapper.readthedocs.org/en/latest/scripts.html#postactivate)

## License

MIT © [Luke Hogan](http://keystrokesofgenius.com)
