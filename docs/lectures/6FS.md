# 6. File System 

##### 05/20/2022 By Angold Wang

**File Systems** is one of the most special place in Operating System, it organize the stored data in hard disk, and maintain the **persistence** so that after a reboot, the data is still available.

The xv6 file system implementation is organized in **seven** layers, shown in the following figure. 

![fslayer](Sources/fslayer.png)

### Layer 1&2: Buffer Cache & Disk Driver
**Accessing a disk is orders of magnitude slower than accessing memory, so the file system must maintain an in-memory cache of popular blocks**, the buffer cache layer caches disk blocks and synchronizes access to them, making sure that only one kernel process at a time can modify the data stored in any particular block.

### Layer 3: Logging
The Logging layer helps the file system to support **Crash Recovery**, that is, **allow higher layers to wrap updates to several blocks in a transactions, and ensures that the blocks are updated atomically in the face of crashes** (i.e., all of them are updated or none).

If a crash (e.g., power failure) occurs, the file system must still work correctly after restart. The risk is that a crash might interrupt a sequence of updates and leave **inconsistent** on-disk data structures (e.g., a block that is both used in a file and marked free).

### Layer 4&5&6&7: Inode & Path
The file system needs on-disk data structures to represent the tree of named directories and files, to record the identities of the blocks that hold each file's content, and to record which areas of the disk are free.

In xv6, each file will be represented as an **Inode**, and the directory is a special kind of inde whose content is a sequence of directory entries. And the pathname layer provides hierachical path names like `/usr/angold/xv6/fs.c`, and resolves them with recursive look up. Finally, at the very top layer, the **file descriptor** abstracts many Unix resources (e.g., pipes, devices, files.) using the lower-layers interface we mentioned above, **simplifying the lives of application programmers.**


### Accumulated Complexity
There are two ways to understand the file system: **Bottom-up** and **Top-down**, we call the former "OS Designer's Perspective" and the latter "Application's Programmer's perspective". 

In the **Top-down** View, each API at the top layer (**`write`**, **`open`**, **`close`**) will be treated as serial instructions, that is: the **call stack** (`fn1()` -> `fn2()` ->... etc,.), which is relatively easy to figure out **how does the fs works** (by going through each routines), but it is very hard to understand **what is the design purpose of each layer** due to the accumlation of complexity at the high level. (it may also costs much time to walk through each
routines, especially in some big
systems)

In the **Bottom-up** View, when you start at the lowest level, the complexity is usually relatively small (code size, less routines...), and one more important thing is that **the higher level usually depends on the lower level underneath, which means after you understand these low-level stuff, the upper layer code seems highly structured.** 

In this article, we will study the xv6 File System in both **Top-down** and **Bottom-up** view in order to have a fully understanding of File System, and answer questions like: **"how does file system works"** and **"why it looks like that (the design choice)"**. I believe the File System is a brilliant example to learn the "Accumulated Complexity" in System Engineering.

## 1. Buffer Cache

## 2. Crash Recovery

## 3. Inode and Path

## 4. System Calls
