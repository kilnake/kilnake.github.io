---
title: Difference between LXC, VM, and Containers in Proxmox
date: 2025-04-27 15:44 +500
categories: [proxmox]
tags: [lxc, vm, container, proxmox]
---

LXC - Lightweight OS Virtualization

VM - Isolated OS Virtualization

Docker - Self Contained Application Environments

## LXC

Your bolting on an OS that uses the same hardware as your host(proxmox). Is going to be much more lightweight and require less storage than a VM, it creates an environment that is a VERY lightweight OS. They have downsides as well. Mostly security related as they share the same kernel as your host, so think of the container as sharing the same brain as your proxmox server. This can be scary at times, as if your proxmox kernel runs into issues, your container can also have issues. While I havent ran into it personally, I was told that kernel updates to Proxmox can botch and break containers SOMETIMES. While it does create a virual OS like a VM does, it does not give you ANY hardware emulation and just uses the hardware your proxmox server does. In general they are more used for instances where you need to conserve on resources, or have a lightweight implementation like a micro service or need to scale efficiently like being able to just create new containers for an app quickly.

## VMS

For VM's your basically running a computer inside your computer. You get a full layer of isolation between the VM and your host (proxmox). So if something happens to your host(proxmox) that would interfere with your application, your VM does not care its isolated, it doesnt touch your proxmox kernel or brain at all. Your downsides are the opposite of the LXC container. Its slower to boot, uses more ram/cpu, needs more configuration. But you get the inherit advantages of full isolation and the ability to fine tune security policies like if you were hosting it on bare metal. Not to mention, you can run entirely different OS's on a VM for example, you can have a windows VM in proxmox but you cant have a Windows LXC, because the LXC has to use linux namespaces same as your host(proxmox) kernel.

## Docker

While it is a container, its really meant to spin up the application part not really the OS part. Docker is a container platform similar to LXC, however LXC is meant to create basically a lightweight OS instead of an application itself. Where docker is really meant for the opposite, its meant to create an environment for an application to run on. Not for an OS to run inside of another OS. Docker is a solution to quick, easy deployment for APPLICATIONS. Not quick easy deployment for OS Virtualization, like LXC would be.

> The fun part about computing is. Its whatever makes sense to your use case, there isnt always a clear cut answer its more pros and cons to each way to do things. {: .prompt-tip }
