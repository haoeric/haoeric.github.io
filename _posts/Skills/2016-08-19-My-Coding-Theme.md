---
layout: post
title: Setup Your Ideal Macbook Terminal in 5 Minutes
comments: true
categories: [Skills]
tags: [terminal, bash, bash-it, macbook, shell, theme]
---

The default setting of the terminal on Macbook acutally is a bit ugly and difficult to use. As shown below:

![raw terminal look](/images/codingTheme/terminal_raw.png)

No much useful prompt message, awkward white background, and won't even close the window after you hit `exit`.  

So here below is my recipe to craft your ideal terminal. In less than 5 minutes, make your terminal environment awesome and consistent accross different devices.

### 1. Install `bash-it`

The defualt shell of macbook terminal is `zsh`, there is a project [oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh) to customize your `zsh`. But I just prefer `bash`, the [bash-it](https://github.com/Bash-it/bash-it) is my choise to make the easy customisation. 

```bash
## install bash-it
git clone --depth=1 https://github.com/Bash-it/bash-it.git ~/.bash_it
~/.bash_it/install.sh
```

### 2. Change Your default Shell to Bash

Under the preference of your terminal, change the shell open with command to `/bin/bash`:

![change default shell](/images/codingTheme/terminal_change_shell.png)

Now you terminal has shifted from `zsh` to `bash`, let's update the theme under bash-it. open `~/.bash_profile` with an editor, find and change the following line

```bash
export BASH_IT_THEME='nwinkler'
```

I have did some change on the `nwinkler` theme to make the prompt more of my preference:

![prompt style](/images/codingTheme/terminal_prompt_style.png)

If you like my setting, you can open the file `~/.bash_it/themes/nwinkler/nwinkler.theme.bash` and replace the content with the following codes.

```bash
#!/bin/bash

PROMPT_END_CLEAN="${green}>${reset_color}"
PROMPT_END_DIRTY="${red}>${reset_color}"

function prompt_end() {
  echo -e "$PROMPT_END"
}

prompt_setter() {
  local exit_status=$?
  if [[ $exit_status -eq 0 ]]; then PROMPT_END=$PROMPT_END_CLEAN
    else PROMPT_END=$PROMPT_END_DIRTY
  fi
  # Save history
  history -a
  history -c
  history -r
  PS1="(\t) $(scm_char) [${cyan}\u${reset_color}@${green}\H${reset_color}] ${yellow}\w${reset_color}$(scm_prompt_info) ${reset_color}\n$(prompt_end) "
  PS2='> '
  PS4='+ '
}

PROMPT_COMMAND=prompt_setter

SCM_THEME_PROMPT_DIRTY=" ${bold_red}✗${normal}"
SCM_THEME_PROMPT_CLEAN=" ${bold_green}✓${normal}"
SCM_THEME_PROMPT_PREFIX=" ("
SCM_THEME_PROMPT_SUFFIX=")"
RVM_THEME_PROMPT_PREFIX=" ("
RVM_THEME_PROMPT_SUFFIX=")"
```

### 3. Setup Terminal Theme

For coding, I like white text with dark blue background, font of `Monaco 12pt`, vertial bar blink cursor in green color. I have wrapped them into my own theme - `Solarized Dark ansi`. And you can download from [here](https://drive.google.com/open?id=0B-Xwi)

Under preference of terminal, goes to profiles, you can load the downloaded theme and set it as default.

![load a new theme](/images/codingTheme/terminal_load_theme.png)

Now you are all done, your terminal should look like this below, enjoy it now.

![final terminal look](/images/codingTheme/iterm_screenshot.png)
