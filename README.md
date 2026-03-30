# Devpod: Base Image (Early attempt)

Devpod base settings for future more customized versions.

Using `mise`, `chezmoi`, and `devcontainers`.

## Prerequisites:

`Docker` and `devpod cli` installed.

## To Use:

Clone the repo onto your machine.

```bash
git clone git@github.com:tanzimul3islam/devpod-base.git .
cd devpod-base
```

Edit the `devcontainer.json` file to set your username.

This will define both the name of the user with `sudo` privileges and the folder structure.

**NB**: The `remoteUser` and the `USERNAME` in the `devcontainer.json` must match.

```
{
  "build": {
    "context": "..",
    "dockerfile": "Dockerfile",
    "args": {
      "USERNAME": "tanzimul"  <--- must match
    }
  },
  "remoteUser": "tanzimul",  <-- must match
  "containerUser": "root",
  "postCreateCommand": "scripts/setup"
}
```

Then run the following commands from within the `devpod-base` folder.

**Caveat**: This assumes you have a dotfiles repo set up for use with `mise`. See [this repo](https://github.com/tanzimul3islam/devpod-dotfiles) for my early attempts at this.

Also, I use `nvim` in my devpods, so my IDE is set to none. Other options include `openvscode` or `vscode`.

The full documentation is available at [https://devpod.sh/docs/what-is-devpod].

```bash
devpod provider add docker
devpod up . --ide none --dotfiles git@github.com:<github_username>/<dotfiles-repo> (--recreate) # start/mount a devpod using the current directory, no IDE set and a specified dotfiles repo. (recreate rebuilds the container)
devpod ssh  # gives a list of available containers to ssh into
```

This is a work in progress and is subject to change without warning or reason.
