---
layout: post
title:  "Mac OS share file with Virtual box"
date:   2016-09-29 +0800
categories: course
---

In the class, we are ask to do simulation on virtual machine and copy the result file to submit.

Since the virtual machine's OS is not uptodate. Teacher did not want us to connect to internet.

I search the result that this way works quiet well with my mac.

With the Virtual Machine powered off and selected in VirtualBox, go to: Machine > Settings ... > Shared Folders
For “Folder Path”, click the icon to browse for the folder you want to share.
For “Folder Name”, enter a name to describe the share.
Click “OK” and start the virtual machine again.
Create a mount point which is basically an empty folder.
Fire up the terminal and type: sudo mount -t vboxsf folder_name path_to_mount_point folder_name is the name you typed in earlier to describe the share
You should be able to browse the shared folder now.