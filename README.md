Gitane
======

Git subtree aliases. Use these shortcuts when dealing with `git subtree` and avoid repetitive strain injuries :no_mouth:

## Installation

You'll probably want to put these shortcuts in your user's global configuration file, typically `$HOME/.gitconfig`, but you can alternatively restrict them to the configuration file under a specific repository (`./git/config`).

Just place the following three aliases in the chosen configuration file under the `alias` section:

```SHELL
[alias]
        st-add = "!f() { \
                DEFAULT_BRANCH=master; \
                DEFAULT_DIR=$(basename $1 | cut -d. -f1); \
                git subtree add --prefix $DEFAULT_DIR $1 ${2:-$DEFAULT_BRANCH} --squash; \
        }; f"
        st-pull = "!f() { \
                DEFAULT_BRANCH=master; \
                DEFAULT_DIR=$(basename $1 | cut -d. -f1); \
                git subtree pull --prefix $DEFAULT_DIR $1 ${2:-$DEFAULT_BRANCH} --squash; \
        }; f"
        st-push = "!f() { \
                DEFAULT_BRANCH=master; \
                DEFAULT_DIR=$(basename $1 | cut -d. -f1); \
                git subtree push --prefix $DEFAULT_DIR $1 ${2:-$DEFAULT_BRANCH}; \
        }; f"
```

You can change the default branch from `master` to anything you wish. You can also remove the `--squash` option if you want to import the entire history from the subproject rather than just a single commit.

## Usage

You start by adding a subproject to your main project:

```SHELL
$ git st-add <remote repository> <optional branch name>
```

Example:

```SHELL
$ git st-add git@github.com:my-org/my-repo.git development
```

This will include `git@github.com:my-org/my-repo.git` (`development` branch) as a subproject in the `./my-repo` directory.

The remaining commands (`st-pull` and `st-push`) are self-explanatory and follow the same syntax.

