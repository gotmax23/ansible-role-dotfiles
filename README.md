# Ansible Role: Dotfiles

[![CI](https://github.com/geerlingguy/ansible-role-dotfiles/workflows/CI/badge.svg?event=push)](https://github.com/geerlingguy/ansible-role-dotfiles/actions?query=workflow%3ACI)

Installs a set of dotfiles from a given Git repository. By default, it will install my (geerlingguy's) [dotfiles](https://github.com/geerlingguy/dotfiles), but you can use any set of dotfiles you'd like, as long as they follow a conventional format.

## Requirements

Requires `git` on the managed machine (you can easily install it with `geerlingguy.git` if required).

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    dotfiles_git: true
Whether or not to clone a git repo to `dotfiles_repo_local_destination` before linking `dotfiles_files`.


    dotfiles_repo: "https://github.com/geerlingguy/dotfiles.git"
    dotfiles_repo_version: master

The git repository and branch/tag/commit hash to use for retrieving dotfiles. Dotfiles should generally be laid out within the root directory of the repository.

    dotfiles_repo_accept_hostkey: false

Add the hostkey for the repo url if not already added. If ssh_opts contains "-o StrictHostKeyChecking=no", this parameter is ignored.

    dotfiles_repo_local_destination: "~/Documents/dotfiles"

The local path from where the `dotfiles_files` will be linked to `dotfiles_home` and where `dotfiles_repo` will be cloned to if `dotfiles_git` is true.

    dotfiles_home: "~"

The home directory where dotfiles will be linked. Generally, the default should work, but in some circumstances, or when running the role as sudo on behalf of another user, you may want to specify the full path.

    dotfiles_dirs: []

List of directories to create in `dotfiles_home` (if any). For example, if you have `.config/mpv/mvp.conf` in `dotfiles_files`, you could add `.config/mpv` to `dotfiles_dirs`.

    dotfiles_files:
      - .zshrc
      - .gitignore
      - .inputrc
      - .vimrc

Which files from the dotfiles repository should be linked to the `dotfiles_home`.

## Dependencies

None

## Example Playbook

    - hosts: localhost
      roles:
        - { role: geerlingguy.dotfiles }

## License

MIT / BSD

## Author Information

This role was created in 2015 by [Jeff Geerling](https://www.jeffgeerling.com/), author of [Ansible for DevOps](https://www.ansiblefordevops.com/).
