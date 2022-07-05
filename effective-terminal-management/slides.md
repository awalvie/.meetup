---
author: awalvie
---

# Effective terminal session management

_Wow, so you like, only use your terminal for everything huh! such hecker, much wow_

## Who Me?

- Name: Vishesh (a.k.a awalvie)
- Work: Resident Permissions Overlord and Part Time SRE @DeepSource
- Dotfiles: github.com/awalvie/dotfiles

---

# Let's get everybody on the same page

- Yes everybody uses VSCode
- Yes its written in Electron, so it's slow as hell _by deisgn_
- Yes new folder, new VSCode window (I'm looking at you Shivam)
- Yes, I'm biased against it, partly because everyone uses it - no variety in life

(If you use a fullblown IDE `my sincere condolences, I'll pray for you`)

---

# Thanks for coming to the session folks, that's it!

...... ...... ...... ......

---

# Alright - fine, it's not all bad

- It's easy to configure
- Lots of extensions
- Can be turned into an IDE
- Opensource
- Simple but powerful
- GUI, so y'know ... everyone likes it

---

# Why turn to the terminal then?

Like every other impoverished broke undergrad student I started with VSCode. But:

- No VSCode if you `ssh` into a server
- New terminal with new `ssh` connection if you want to run a second command
- No mouse in `ssh`
- Doesn't ship by default on most distributions, have to install it
- Just felt clunky and slow in general
- Usually had a separate terminal emulator with multiple windows running and used VSCode exclusively as the editor
- It started feeling really boring and annoying to use

Wheere lieth the the promised land

---

# Receipe

**Nutrition Info**

- **Prep Time**: Depends how long you can run `:h command` on vim before loose sanity
- **Servings**: One - only you understand your dotfiles, you wrote em
- **Yield**: You get to tell everybody why their setup is trash

**Ingredients**

- VIM
- TMUX
- `ln -sf`

**Directions**

- Install VIM
- Install TMUX
- ....
- Profit

---

# Demo

Let's give you a quick taste of what you get with VIM and TMUX

## Why only limit yourself to the terminal

**ALL HAIL VIMIUM-C**

---

# Quick dive into what the dots look like

---

# How can you get started?

## VIM

- [ ] Basics First! `vimtutor` is your friend
- [ ] Set `capslock` to `escape` unless you want your pinkie finder to be longer than all the others
- [ ] https://vimconfig.com/ to write a barebones vim config file
- [ ] Figure out how to get help when stuck; `:h` command is your friend
- [ ] Time to install some plugins: https://vimawesome.com/

## TMUX

- [ ] **PSA**: The default `mod` key `C-b` sucks - get a different one
- [ ] Basics First, Electric Boogaloo! You don't need no guides, get a TMUX cheatsheet and you should be good to go!
- [ ] https://tmuxguide.readthedocs.io/en/latest/tmux/tmux.html time to read some docs
- [ ] Or ~~steal~~ borrow from other's dotfiles!

---

# Questions!
