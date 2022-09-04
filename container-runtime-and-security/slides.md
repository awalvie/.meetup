---
author: awalvie
---

# ~~Fortifying container runtime and security on Kubernetes~~

## Who Me?

- Name: Vishesh / Vineesh / Vinesh / Bineesh
- Work: VIM Philantrophist - Evangalist and Part-Time Infrastructure Engineer @ DeepSource

---

## Audience Poll

- How many of us use containers daily?
- How many of us use docker for our containers?
- How many of us here use kubernetes?

---

## That's a lot of you, time for a pop quiz

- What's docker?
- What's a container image without using docker?

---

## Docker

- Docker is a Container Engine
- It builds images with Dockerfiles which are OCI Standard compliant via BuildKit
- Docker internally makes use of a Container Runtime like `runc` which _runs_ the container

---

## Now what are container images?

drumroll

. . . .

. . . .

. . . .

tarballs ... or more accurately a stack of tarballs

---

## So how do we go from folders –> something running

Glad you asked


---

## Step 1 - Grab yourself an image


---

## Step 2 - Look at what's inside

It looks familiar right?

There's

- `/bin`
- `/etc`
- `/boot`
- `/proc`

You've seen this before, it looks like the linux filesystem doesn't it

---

## Step 3 - Linux magic

- Lets restrict the view of the filesystem. We'll use using a command called `chroot`.

```bash
$ sudo chroot rootfs /bin/bash
```

The command changes the root folder for the current process, hence `ch - root`.

- Why does this work though? We don't have any access to the host filesystem how are we able to run commands?

Will this command work or fail?

```bash
$ sudo chroot rootfs python2 -m SimpleHTTPServer

```

---

## What can we do from here

- Lets run a command outside the chroot

```bash
# outside chroot
$ top
```

- Can the `chroot` see this process?

```bash
$ sudo chroot rootfs /bin/bash
$ mount -t proc proc /proc
$ ps aux | grep -i top
```

- It can! Can I kill that process?

```bash
$ pkill top
```

- And there it goes so much for containarization, why is the chrooted process able to kill the parent process?

Because it inherits the process tree of the parent process. We need some way of isolating the view the child process has to the parent process tree


---

## Step 4 - Creating and entering namespaces

- Namepsaces can restrict the information a process has to things like network interfaces, mounts and most importantly process trees!

We can use the unshare command to create a new PID namespace and mount a `proc` filesystem to it

```bash
$ sudo unshare -p -f --mount-proc=$PWD/rootfs/proc \
    chroot rootfs /bin/bash
```

- Run `top` and our process things it's PID 1!

---

## Step 5 - Now how do I join this namespace


Namepaces can be shared around! Processes can share the same namespace or be separate from specific namespaces

- Lets find the process running the `chroot`

```bash
$ ps aux | grep /bin/bash | grep root
```

- Lets get it's PID and and find it's namespaces. Namespaces can usually be found under `/proc/(PID)/ns`

```bash
$ sudo ls -l /proc/{PID}/ns
```

- We can then use another linux command `nsenter` to enter this respective namespace

```bash
$ sudo nsenter --pid=/proc/{PID}/ns/pid \
    unshare -f --mount-proc=$PWD/rootfs/proc \
    chroot rootfs /bin/bash
```

---

## Step 6 - Getting fancy with cgroups

`cgroups`, short for control groups, allow kernel imposed isolation on resources like memory and CPU.

Sure we've isolated processes but we can just as well spawn a process that consumes all the existing memory.

- The kernel exposes cgroups through the `/sys/fs/cgroup` directory, lets take a look!

We can use `cgroups` to configure things like CPU, Memory allocation limits etc.


---

## Why the long way around?

---

## I thought this was a talk about container security? When does that start?

- Lets go to the docs: https://kubernetes.io/docs/tasks/configure-pod-container/security-context/


---

# Reference

- https://developers.redhat.com/blog/2018/02/22/container-terminology-practical-introduction
- https://ericchiang.github.io/post/containers-from-scratch/
- https://fly.io/blog/sandboxing-and-workload-isolation/

