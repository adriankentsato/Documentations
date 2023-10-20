# Setting up MSYS

Please see [Microsoft Windows Development Setup | MSYS Installation](./Windows%20Development%20Environment.md#msys2-installation) for instructions on how to install MSYS.

## Initialize and Update MSYS

Go to MSYS installation folder and open `msys2_shell.cmd`. It would take time to initialize the environment, so we'll be patient.

Once it is done initializing, enter these commands to get the environment up to date.

```bash
pacman -Syuu
pacman -Su vim openssh
pacman -Syuu
```

## Setup SSH Keys for GitHub use

Paste the command below, substituting in your GitHub email address.

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"

# if system does not support ED25519 algorithm use the one below
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

You will be prompted to enter where you want the keys to be stored. If you wanted for the keys to be password protected, enter your desired password when asked.

Follow the instructions defined in this [GitHub Docs | Add SSH Key to GitHub](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account) to add your newly generateed SSH Key to GitHub.

## Setup terminal PATH and automation

Open `~/.bashrc` using vim, and append this code to the end of the file.

<details>
    <summary>.bashrc File</summary>

```bash
# This is the .bashrc file for the msys distro

export PATH=$PATH:/c/sw/git/bin

# setup ssh-agent and prevent multiple instance
env=~/.ssh/agent.env

agent_load_env () { test -f "$env" && . "$env" >| /dev/null ; }

agent_start () {
    (umask 077; ssh-agent >| "$env")
    . "$env" >| /dev/null ; }

agent_load_env

# agent_run_state: 0=agent running w/ key; 1=agent w/o key; 2=agent not running
agent_run_state=$(ssh-add -l >| /dev/null 2>&1; echo $?)

if [ ! "$SSH_AUTH_SOCK" ] || [ $agent_run_state = 2 ]; then
    agent_start
    ssh-add -t 600 ~/.ssh/rsa
elif [ "$SSH_AUTH_SOCK" ] && [ $agent_run_state = 1 ]; then
    ssh-add -t 600 ~/.ssh/rsa
fi

unset env
```
</details>

