<!-- Bash Profile settings -->

```css
# ----------------------
# Git Aliases
# ----------------------

alias gs='git status'
alias ga='git add'
alias gaa='git add .'
alias gcm='git commit -m'
alias gi='git init'
alias gcl='git clone'
alias gl='git log'
alias gpl='git pull'
alias gpsh='git push'
alias gco='git checkout'
alias gb='git branch'
alias grt='git reset'
alias gst='git stash'
alias gstp='git stash pop'
alias gdf='git diff'
alias cls='clear'
alias cd..='cd ..'
alias c='code .'
alias gcm1='git commit --date="1 day ago" -m'
alias gcm2='git commit --date="2 day ago" -m'
alias gcm3='git commit --date="3 day ago" -m'

# ----------------------
# Prompt style
# ----------------------

if test -f /etc/profile.d/git-sdk.sh
then
    TITLEPREFIX=SDK-${MSYSTEM#MINGW}
else
    TITLEPREFIX=$MSYSTEM
fi

if test -f ~/.config/git/git-prompt.sh
then
    . ~/.config/git/git-prompt.sh
else
    PS1='\[\033]0;Git Bash\]' # set window title
    PS1="$PS1"'\n'                 # new line
    PS1="$PS1"'\[\033[0;35m\]'       # change to purple
    PS1="$PS1"' '
    PS1="$PS1"'[\A] - \u '             # time@user<space>
    # PS1="$PS1"'\[\033[35m\]'       # change to purple
    # PS1="$PS1"'$MSYSTEM '          # show MSYSTEM
    PS1="$PS1"'\[\033[33m\]'       # change to white
    PS1="$PS1"'\w '                 # current working directory


    if test -z "$WINELOADERNOEXEC"
    then
        GIT_EXEC_PATH="$(git --exec-path 2>/dev/null)"
        COMPLETION_PATH="${GIT_EXEC_PATH%/libexec/git-core}"
        COMPLETION_PATH="${COMPLETION_PATH%/lib/git-core}"
        COMPLETION_PATH="$COMPLETION_PATH/share/git/completion"
        if test -f "$COMPLETION_PATH/git-prompt.sh"
        then
            . "$COMPLETION_PATH/git-completion.bash"
            . "$COMPLETION_PATH/git-prompt.sh"
            PS1="$PS1"'\[\033[36m\] '  # change color to cyan
            PS1="$PS1"'[git:`__git_ps1`]'   # bash function
        fi
    fi
    PS1="$PS1"'\[\033[0m\]'        # change color
    PS1="$PS1"'\n'                 # new line
    PS1="$PS1"'➜ '                 # prompt: always $
fi

MSYS2_PS1="$PS1"               # for detection by MSYS2 SDK's bash.basrc

# Evaluate all user-specific Bash completion scripts (if any)
if test -z "$WINELOADERNOEXEC"
then
    for c in "$HOME"/bash_completion.d/*.bash
    do
        # Handle absence of any scripts (or the folder) gracefully
        test ! -f "$c" ||
        . "$c"
    done
fi

# ----------------------
# Git status options
# ----------------------
export GIT_PS1_SHOWSTASHSTATE=true
export GIT_PS1_SHOWDIRTYSTATE=true
export GIT_PS1_SHOWUNTRACKEDFILES=true
export GIT_PS1_SHOWUPSTREAM="auto"


```
