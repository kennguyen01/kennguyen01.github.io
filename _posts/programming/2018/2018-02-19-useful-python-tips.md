---
title: Useful Python Tips
date: 2018-02-19
categories: programming
---

This is a collection of some useful Python tips since I first started learning the language. I found out about them through different projects, online courses, and code challenges. The caveat is that they are a bit all over the place. They range from setting up a virtual environment to more general Python tips. As I learn more about the language, I will update this post.

<!--more-->

Before we start, I do want to say ahead of time that I will be using Python 3 and my OS is Ubuntu. When I use the terminal to type in command lines, it will be written for Linux.

## Deque

`deque` is a container datatype alternative to `list`. The main difference between them is that deque has O(1) time complexity for both `append` and `pop` from both sides of the queue. While list is O(1) for the end but O(n) for beginning. You can read more about deque here: [Deque](https://docs.python.org/3.6/library/collections.html#collections.deque).

Now let’s see a simple example of deque in action. Suppose you want to remove the first element of a list and move the second element to the end. Then repeat the process until only one element is left and return it.

```python
from collections import deque

def delete_swap(L):
    l = deque(L)
    while len(l) > 1:
        l.popleft()
        v = p.popleft()
        l.append(v)
    return l[0]
```

## Dictionary

### Merge Two Dictionaries
In Python 3.5 and above, you can merge two dictionaries together in a single expression.

```python
c = {**a, **b}
```

What’s cool about this expression is that you can perform dictionary comprehension on each of those dictionaries before merging them together. For a problem set of a MOOC I took, I had to create a dictionary of a [Caesar Cipher](https://en.wikipedia.org/wiki/Caesar_cipher) program that applies cipher to a message. The amount of shift is how much the letter is moved down the alphabet. A shift of one means that letter key `"a"` will be mapped to another letter, `"b"` in this case.

The function returns a dictionary of 52 keys, 26 for each lowercase and uppercase letters. What I did was to use dictionary comprehension for each dictionary’s shift while merging both of them together to a new dictionary:

```python
import string

def shift_dict(shift):
    lower = string.ascii_lowercase
    upper = string.ascii_uppercase
    letter_map = {
        **{k: lower[(i + shift)%26] for i, k in enumerate(lower)},
        **{k: upper[(i + shift)%26] for i, k in enumerate(upper)}
    }
    return letter_map
```

## PIP

`pip` is a command line tool for managing your Python packages. If you have Python 3.4 and above, pip should already come pre-installed. If you don’t have it, just open up the terminal and type in:

```shell
$ sudo apt install python3-pip
```

Then to install packages you can simply type this into the terminal:

```shell
$ pip3 install <package>
```

You can also install a package with `sudo apt install python3-<package>` but pip is a cleaner way to install packages. Pip also install any dependency that a package needs when you run it. Of course you can also install a package manually by downloading the `tar.gz` file but it’s a hassle because you have to unzip it and move the files to the intended directory. It’s better to use pip and save yourself the headache.

If you want to see other pip commands, type `pip3 --help`.

## Virtual environment

`virtualenv` allows you to create a copy of Python installation on a specific directory. To install it, you just use pip:

```shell
$ pip3 install virtualenv
```

The good thing about virtualenv is that packages you installed in the virtual environment will not affect the global packages on your system. For example, you are starting a new project and you need to install packages specific to the project, you can `cd` into the project directory and create a virtual environment inside:

```shell
$ python3 -m venv <dir_name>
```

When you check inside the project folder, there should be a new directory called `dir_name`. It is an isolated Python environment for locally installed packages. To make matter simple, I will use `venv` as the name of your virtual environment. You can then use the virtual environment by activating it:

```shell
$. venv/bin/activate
(venv)$ 
```

The `(venv)` in the terminal shows that the virtual environment has been successfully activated. Now if you want to install `matplotlib` to plot data points for this project, you just install it normally with pip:

```shell
(venv)$ pip3 install matplotlib
```

And when you are done with installing local packages, you deactivate the virtual environment:

```shell
(venv)$ deactivate
$
```

Remember that the virtual environment is simply directory on your system. If you don’t need it anymore, you can remove it:

```shell
$ rm -rf venv
```

## Specific Python Version

### Installing pyenv

To use a specific version of Python when working on a project, use [pyenv](https://github.com/pyenv/pyenv). The simplest way to install it is by using [pyenv-installer](https://github.com/pyenv/pyenv-installer).

Before installing `pyenv-installer`, we need to install some dependencies:

```shell
$ sudo apt install -y build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev libncursesw5-dev xz-utils tk-dev libffi-dev liblzma-dev python-openssl git
```

Then run:

```shell
$ curl https://pyenv.run | bash
$ exec $SHELL
```

But the path will not be exported to `.bashrc` so you need to do that:

```shell
$ echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
$ echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
$ echo -e 'if command -v pyenv 1>/dev/null 2>&1; then\n eval "$(pyenv init -)"\nfi' >> ~/.bashrc
$ exec $SHELL
```

You can check the version and update with:

```shell
$ pyenv version
$ pyenv update
```

### Uninstall pyenv

To remove pyenv:

```shell
$ rm -rf ~/.pyenv
```

And remove the lines below from `.bashrc`:

```shell
export PATH="$HOME/.pyenv/bin:$PATH"
eval "$(pyenv init -)"
eval "$(pyenv virtualenv-init -)"
```

Then restart with `exec $SHELL`.