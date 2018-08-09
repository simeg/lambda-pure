# λ Pure

> Pretty, minimal and fast ZSH prompt based on Pure

<img src="screenshot.png" width="864">


## Overview

Most prompts are cluttered, ugly and slow. I wanted something visually pleasing that stayed out of my way.

### Why?

- Comes with the `λ` prompt character. Because lambdas are cool.
- Shows `git` branch and whether it's dirty (with a `×`).
- Indicates when you have unpushed/unpulled `git` commits with up/down triangles. *(Check is done asynchronously!)*
- Shows current NodeJS version on the right side. *(Check is done asynchronously!)*
- Prompt character turns red if the last command didn't exit with `0`.
- Command execution time will be displayed if it exceeds the set threshold.
- Username and host only displayed when in an SSH session.
- Shows the current path in the title and the [current folder & command](screenshot-title-cmd.png) when a process is running.

## Install

Can be installed with `npm` or manually. Requires git 2.0.0+ and ZSH 5.0.0+.

### npm

```console
$ npm install --global lambda-pure-prompt
```

That's it. Skip to [Getting started](#getting-started).

### Manually

1. Either…
  - Clone this repo
  - add it as a submodule, or
  - just download `lambda-pure.zsh` and `async.zsh`

2. Symlink `lambda-pure.zsh` to somewhere in [`$fpath`](https://www.refining-linux.org/archives/46-ZSH-Gem-12-Autoloading-functions.html) with the name `prompt_lambda-pure_setup`.

3. Symlink `async.zsh` in `$fpath` with the name `async`.

#### Example

```console
$ ln -s "$PWD/lambda-pure.zsh" /usr/local/share/zsh/site-functions/prompt_lambda-pure_setup
$ ln -s "$PWD/async.zsh" /usr/local/share/zsh/site-functions/async
```
*Run `echo $fpath` to see possible locations.*

For a user-specific installation (which would not require escalated privileges), simply add a directory to `$fpath` for that user:

```sh
# .zshenv or .zshrc
fpath=( "$HOME/.zfunctions" $fpath )
```

Then install the theme there:

```console
$ ln -s "$PWD/lambda-pure.zsh" "$HOME/.zfunctions/prompt_lambda-pure_setup"
$ ln -s "$PWD/async.zsh" "$HOME/.zfunctions/async"
```


## Getting started

Initialize the prompt system (if not so already) and choose `lambda-pure`:

```sh
# .zshrc
autoload -U promptinit; promptinit
prompt lambda-pure
```


## Options

### `PURE_CMD_MAX_EXEC_TIME`

The max execution time of a process before its run time is shown when it exits. Defaults to `5` seconds.

### `PURE_GIT_PULL`

Set `PURE_GIT_PULL=0` to prevent Pure from checking whether the current Git remote has been updated.

### `PURE_GIT_UNTRACKED_DIRTY`

Set `PURE_GIT_UNTRACKED_DIRTY=0` to not include untracked files in dirtiness check. Only really useful on extremely huge repos like the WebKit repo.

### `PURE_GIT_DELAY_DIRTY_CHECK`

Time in seconds to delay git dirty checking for large repositories (git status takes > 2 seconds). The check is performed asynchronously, this is to save CPU. Defaults to `1800` seconds.

### `PURE_PROMPT_SYMBOL`

Defines the prompt symbol. The default value is `λ`.

### `PURE_GIT_DOWN_ARROW`

Defines the git down arrow symbol. The default value is `▼`.

### `PURE_GIT_UP_ARROW`

Defines the git up arrow symbol. The default value is `▲`.

### `PURE_GIT_DIRTY`

Defines the git dirty symbol. The default value is `×`.

### `PURE_NODE_ENABLED`

Set `PURE_NODE_ENABLED=0` to not display the NodeJS version.

## Example

```sh
# .zshrc

autoload -U promptinit; promptinit

# optionally define some options
PURE_CMD_MAX_EXEC_TIME=10

prompt lambda-pure
```

## Integration

### [oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh)

1. Symlink (or copy) `lambda-pure.zsh` to `~/.oh-my-zsh/custom/themes/lambda-pure.zsh-theme`.
2. Set `ZSH_THEME="lambda-pure"` in your `.zshrc` file.

### [antigen](https://github.com/zsh-users/antigen)

Update your `.zshrc` file with the following two lines (order matters). Do not use the `antigen theme` function.

```console
$ antigen bundle mafredri/zsh-async
$ antigen bundle marszall87/lambda-pure
```

### [antibody](https://github.com/getantibody/antibody)

Update your `.zshrc` file with the following two lines (order matters):

```console
$ antibody bundle mafredri/zsh-async
$ antibody bundle marszall87/lambda-pure
```

### [zgen](https://github.com/tarjoilija/zgen)

Update your `.zshrc` file with the following two lines (order matters):

```console
$ zgen load mafredri/zsh-async
$ zgen load marszall87/lambda-pure
```

## License

MIT © [Michał Nykiel](https://github.com/marszall87)
based on [Pure by Sindre Sorhus](https://github.com/sindresorhus/pure)
