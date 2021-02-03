---
title: Adding Disks to ASM
author: Kishan Parekh
date: 2021-01-18 19:00:00 -0500
categories: [Blogging, ASM]
tags: [oracle, asm]
image: /assets/img/images/asm_overview.jpg
---

# ASM Disks

As a brief overview, Oracle Automatic Storage Management (ASM) is an integrated, high-performance database file system and disk manager. More information on this can be found on the official documentation [here.](https://docs.oracle.com/cd/E11882_01/server.112/e18951/asmcon.htm#OSTMG036)

## Outline

The purpose of this post is to show how to add more disk space to an existing ASM system. This is a common enough procedure on Unix based systems, but on Windows, there are some additional steps to be aware of.

- Add disk space
- Create Logical Partitions
- Label the Partitions
- Add to ASM Storage
- Verify partitions were added

### Add Disk Space in Windows

Adding disk space depends on how the system is set up.
If this is a VM, then it might simply be a matter of mounting a new disk. If a physical device needs to be added, then we'd have to ensure it is compatible.

For the purposes of this post, and from my testing, we are going to assume the space has already been added to the VM. Once the disk has been added, it should be listed as a New Volume, and show up as a Basic Drive.

Check current space in Windows Disk Management:
![Example of Disk Management](/assets/img/images/diskmgmt.png)

### Create Logical partitions

Now that we have the disk space added to the machine, we have to create logical partitions. Oracle ASM only works on partitioned disks in Windows.  
The only partitions that OUI displays for Windows systems are logical drives that are on disks and have been marked (or stamped) with asmtool or by Oracle ASM Filter Driver.

1. Open Command Prompt using "Run as Administrator"
1. Start diskpart tool

            ```c:/> diskpart
            ```

1. Verify current disks

          {% highlight bash linenos %}
          c:/> diskpart
          {% endhighlight %}

1. A test
