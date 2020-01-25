# gitfiles

These are configurations for `git`.

Run on a sh-compatible terminal (for a quick install):

    sh ./pre-setup.sh

This will install (hopefully) `rcm` if you don't have it and then configure
everything with it using the tag `git`.

If you want to update, then pull from the git repository and run the
`pre-setup.sh` script again.

If you want to know what's happening inside (or are using a linux different than
voidlinux), then:

## Pre-requisites

Clone into your terminal:

    git clone git://github.com/nrxr/gitfiles.git \
      ~/code/src/github.com/nrxr/gitfiles

Install [`rcm`](https://github.com/thoughtbot/rcm):

    # macOS
    brew tap thoughtbot/formulae
    brew install rcm

    # voidlinux
    sudo xbps-install -S rcm

## Installing the `git` configuration files with `rcm`

    rcup -d $HOME/code/src/github.com/nrxr/gitfiles \
      -v -t git \
      -x README*.md -x LICENSE -x pre-setup.sh

Manually updating can be done by running `pre-setup.sh` again or this same line.

## How to use this correctly

If you check the actual `gitconfig`, you'll find there's an `include` directive
that points to `~/.gitconfig-private` and inside that what I have is conditional
includes depending on the `gitdir`. So something like:

    [includeIf "gitdir:~/work"]
      path = ~/.gitconfig-work

What I have there is different name, email and URL redirects. What? Yes: URL
redirects, like:

    [url "git@work-github.com"]
      insteadOf = git@github.com
    [url "https://user:personaltoken@github.com"]
      insteadOf = https://github.com

In turn, inside `~/.ssh/config` I have entries for `work-github.com` that will
use the `IdentityFile` that's in my work account. That way I can handle multiple
github accounts in a transparent manner.

No changing URLs while cloning, not remembering what's the cute little name I
made up for my work, my hobby, my personal account. Nope. Just transparent
handling.

## License

© 2020, nrxr `<nrxr@disroot.org>`. Released under the MIT license terms.
