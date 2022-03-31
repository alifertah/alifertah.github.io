---
title: what we do the wrong way
layout: post
tags: 1337 git clang
category: school
---

42 network have one the most effective cursus in the world. the people behind it are smart people
and know what they are doing.
 while the cursus can teach you about some important technical areas in computer science.
 you might not learn how to write a better code, and follow best practices.

## Git the right way
This tool is abused by many students, this is my second fav software ever
and I feel bad when the most important tool in devpack used
in arbitrary way. here is some common points I noticed And I took personally:

### git add .
It's easier to add files to stage area using this approach. just stage everything .DStore and all other useless garbage files.

**NOOOOOOOOOOOOO Please**, just add files that are neccessary for your project. you might be to lazy to stage them one by one,
 just use Vscode or to be fast use [Fugitive plugin](https://github.com/tpope/vim-fugitive) in vim.

With this you can make sure that you only have neccessary files in your repo, and give you a better understanding for
changes you made so you can have a well-written commit message.

### git status \n git commit -m "whatever"
I can't call this 'abuse' but it's much better to just use `git commit` and this will show you a useful status in your
favorite editor(vim), write down a useful message, save&quit and your commit will be done.

isn't it much easier to write a commit message while you can see files that you changed ?

**Example:**

```bash
$ git commit
```

this will open vim where you can write your commit msg:
* :q -> quit to abort commit
* :wq -> save&quit to save commit

```
my useful commit message here
# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# On branch main
#
# Initial commit
#
# Changes to be committed:
#	new file:   file1
#	new file:   file2
#
```

### git clone && mv ur files
When they finished thier project. most students realise that they didn't link it with vogsphere.
They do what I call a smart move, just clone it and move file from project to cloned repo.

Guess what stupid? git remote is much easier.

```
$ cd myproject
$ git remote add intra [link to vogsphere repo]
$ git push -u intra master
```
Now you can look for evalutors.

### gitignore
This file is freaking useful to avoid staging useless files.

Files you might want to put in `.gitignore` file:

```
.gitignore
*.o
build/
libft.a # or any binary file you have in your project
```

## Makefile (the same everywhere)
Take makefile from prevouis project change your source files and Header file. run it, and magically it works.
Hell noooooo, makefile has a lot to learn.

### No source files in makefile

You should never put source files in your makefile, why? because you will never need them. your are just risking deleting them
with a stupid mistake that we as developer like to do.

so instead of this

```make
SRC = main.c lkiks.c
OBJ = $(SRC:.c=.o)
```

what about this smart genuis idea:

```make
OBJ = main.o lkiks.o
```

[Example from linux kernel](https://github.com/torvalds/linux/blob/master/fs/fuse/Makefile).

### Object file? In root directory???
I hate to see object files in the root directory, running `make fclean` everytime you are looking
for a file, this elimante the role of makefile in first place(relink).

**Solution:**
I am sure that this is the best way but at least I think it works almost perfectly for small projects.
Your object files should be inside a folder called `build` 

```
build
├── checker
│   ├── checker.o
│   └── exec.o
├── common
│   ├── stack
│   │   ├── instructions.o
│   │   ├── op.o
│   │   ├── swap.o
│   │   ├── swipedown.o
│   │   └── swipeup.o
│   ├── str.o
│   └── utils.o
└── pushswap
    ├── main.o
    ├── opti.o
    ├── sort_5.o
    ├── stack_sort.o
    └── utils
        └── misc.o
checker
├── checker.c
├── exec.c
└── inc
    └── checker.h
common
├── stack
│   ├── instructions.c
│   ├── op.c
│   ├── swap.c
│   ├── swipedown.c
│   └── swipeup.c
├── str.c
└── utils.c
pushswap
├── inc
│   └── stack.h
├── main.c
├── opti.c
├── sort_5.c
├── stack_sort.c
└── utils
    └── misc.c
```

**Example:**
This [my Makefile](https://gitlab.com/abellaismail/pushswap/-/blob/main/Makefile) for pushswap project;

And it's a great example for reusing component in your project too.

## Learn shell
In the first 2 days in the pool you learned about shell. but most of student don't apply what they learned
to do repeatable task.

Ohmyzsh comes with great start point for you, but I always recommand to have your own configuration cuz why not.
here is [my minimal configuration](https://github.com/abellaismail7/.dotfiles/blob/main/.config/zsh/.zshrc)
if you need inspiration.

### Example
Here is some aliases you might need:

open `~/.zshrc` and add this lines
```bash
alias g='git'
alias ga='git add'
alias gs='git status'
alias gc='git checkout'
alias gco='git commit'
alias gp='git push'

alias v='vim'

alias -- l='ls -lah'
alias -- ll='ls -lAh'
alias -- ls='ls --color=auto'
alias -- md='mkdir -p'

alias -- -='cd -'
alias -- ..='cd ..'
alias -- ...='cd ../..'
```

```bash
$ touch file1 file2 # instead of 
$ ga file1 file2 # instead of git add 
$ gs # instead of git status
On branch main

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   file1
	new file:   file2

$ gc -m ""
```

## Even C?
While C is the core of the cursus there some common problems I and students made and still.

### Learn C not norm
In general I like the norm. but most of new student never heard of a lot of keywords/functions in c
You might not know that there is scanf to read from stdin. You might not know about for loops.

Some students never heard of allowed features in c like struct/enums/union ...;

Investing some time learning the practical C will help you write tests faster saving you some time.

### Never use write directly (or waste your time)
Prevent students from using stdio functions is just a genuis idea.
while we have functions like open, read and write that are intract directly with system ...
but using write directly is a bad idea cuz it's error-prone, we developers like to make dump mistakes.
for me I like to use `ft_putstrfd(int fd, char *s)`.

### Programming is like mariage, you are always wrong.
You can insult iMac and c as you can, but most of the time you doing something wrong.
we are using c89 compiled using gcc which is one of the most mature projects.
written by genuis people so It's more likely you doing it wrong.

### Once it works don't touch it mindset.
What a pure bad mindset to have as developer.
refactoring(the process of making code better) is one of the most important skills as software eng.
here is a qoute from kent beck

> Make it work, make it right, make it fast. 
-- Kent Beck 

I highly recommand two books:

1. [clean code, uncle bob](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882) : This will teach you how to write an understable, readable code. 
1. [Refactoring, martin fowler](https://martinfowler.com/books/refactoring.html) : This will teach you how to rewrite part of you code to be better and faster.

## In The end
This is what I think. If you have a different opinion we can discuss it in my twitter account (link below)
If you want to add anything to this feel free to pull request in [this repo](https://github.com/abellaismail7/abellaismail7.github.io).