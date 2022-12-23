## Introduction

![image](https://user-images.githubusercontent.com/54491362/207887410-0e927cdb-7351-4deb-bcd3-8db77c5d0abe.png)

- default: Ext4
- Use VirtualBox to install Linux as a VM on your computer

- Linux has multiple consoles: tty1 - tty7 (can be upto tty12)
- tty12 is the GUI
- Remote terminals (When using a remote connection via shh): pts - Pseudo Terminal Slave - It is showed along with the IP address that is logged in

- Find out who is logged in: `who` 
- ![image](https://user-images.githubusercontent.com/54491362/207893450-050a916e-6ed3-46e9-96e6-c7060bd1710a.png)
- ![image](https://user-images.githubusercontent.com/54491362/207893519-3c20bf47-a829-432b-96cc-63cf92caa7e0.png)

- Documentation of a tool x: `man x` (pgup/pgdwn/up/dwn//search), `help`, `info`
  - man pages are divided into sections
- Search for a tool to do y: `apropos y`
- Get oneliner explanation for commands: `whatis x`


## File System
![image](https://user-images.githubusercontent.com/54491362/207903995-7d59e7eb-8fa8-45c9-b860-53a816e2a7c4.png)
![image](https://user-images.githubusercontent.com/54491362/207904179-bc19007b-d4e6-40a4-ad38-7d8d40bbd6f0.png)
![image](https://user-images.githubusercontent.com/54491362/207904477-45e68eca-223d-48a8-8d73-20806504eaf3.png)

-Find out where a command is stored: `which <command>`
- List files: `ls [-l] [-a] [-r]`
- Files starting with . are hidden and shown when `ls -a`
- Show the type of file: `file <file>`

### Text Editors
- Vim: Complex and powerful
- Nano: Simple

### Links 

1. Hard Links
Data on disk is stored in different blocks. And these block ids are stored in a datastructure called inode. Files links to the inode using a hardlink. That's why even if you change the name of the file the file is still available at the location, you don't break the link. Note that copying the file creates a separate inode as the data is also copied.

2. Soft Link
Here the link is pointing to the file name rather then the inode. Because of this, if you change the file name, the link breaks

![image](https://user-images.githubusercontent.com/54491362/209195843-fd34cf2c-e5be-43f7-bbfb-07c8b2b38837.png)

- Create a soft link: `ln -s <absolute path to original file> <link path to file>`
- Create a hard link: `ln <path to original file> <link path to file>`

![image](https://user-images.githubusercontent.com/54491362/209197271-b168ca16-bf10-4347-9ced-cf1bb2b19a42.png)
- These numbers indicate the number of hard links to the inode of that file. 

### Find files
- Create files with a certain amount of space: `truncate -s <desired_size> <desired_file_name>`
- To find a file `find <path_to_start_search> [-name | -type | -size] <argument>` (You can use globbing here `find . 'cat-*'`)
- Find the difference betweent two text files: `diff [-y | -u] <file1>.txt <file2>.txt`
- Find the difference between two non-text files: `cmp <file1> <file2>`
- Information about a file: `stat <file>`

### Input/output redirection
- Consoles: Std. Error - 2; Std. Output - 1, Std. Input - 0
- To redirect output to a file, `'some_command' 'console_no'> 'inputfilename'`
- To redirect to a command, `command1 | command2 | command3` will chain them together
- `>` overwrites existing content, `>>` appends to the existing content
- You can input to a command from a file by using `<`
- You can input to a command from a console by using the "here file" operator `<< EOF` To exit type 'EOF'

### Compressing and decompressing files
- Archiving: Converting multiple files to a single file for portability -> .tar
- Compressing: Reducing size by encoding info: Lossy and Lossless (default)
- Two kinds of compressed format: .tgz and .zip
- Create Archive: `tar -cf <tar_file>.tar <globbed_files_to_archive>`
- Extract archive or compressed tgz: `tar -xf <tar_file> [-d <target_dir_name>]`
- Create tgz: `tar -czf <tgz_file> <globbed_files_to_archive> [<globbed_files_to_archive>]`
- Create zip: `zip <target> <files>`
- Unzip zip: `unzip <zip_file>`








