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

### Find files and text
- Create files with a certain amount of space: `truncate -s <desired_size> <desired_file_name>`
- To find a file `find <path_to_start_search> [-name | -type | -size] <argument>` (You can use globbing here `find . 'cat-*'`)
- Find the difference betweent two text files: `diff [-y | -u] <file1>.txt <file2>.txt`
- Find the difference between two non-text files: `cmp <file1> <file2>`
- Information about a file: `stat <file>`
- Find a text inside a file: `cat <file> | grep [-E] <pattern>` Use `-E` for using regex

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
- `c`: create, `f`: file (normally to stdout), `z`: tgz

### Reformat or edit text
- Use `sed` for editing and `awk` for reformatting and rearranging
![image](https://user-images.githubusercontent.com/54491362/209274379-933410c7-9357-47fb-ba82-903c984de649.png)
- sed pattern: `s/<pattern>/<replace_content>[/g]` `g` is used for replacing all. Default is to replace the first occurrence on every line.
- awk pattern: `$<n>`: nth word

- Use `sort` and `uniq` to sort the output and get unique values from it respectively
- Use `sort -n` for numeric sort. Otherwise normal string sort is done
- Use `cut -d <delimiter> -f <column_no> <file>` to find a column from a delimitered file like csv

## File Permissions
- Format of ls -l: `<type><user_perm><group_perm><other_perm> <no_of_hard_links> <user_name>  <group_name>`
- perm: `rwx` (Read Write execute)
- Eg. \_rw_r_xr__ :
    - It is a file
    - Owner can Read and Write
    - Group can Read and Execute
    - Others can only Read
 
- ![image](https://user-images.githubusercontent.com/54491362/210047493-335be08c-9a86-4328-999d-c3b6066e3c0b.png)

- Permission in octal notation
- ![image](https://user-images.githubusercontent.com/54491362/210047578-bf738248-d783-42e0-8014-2580c4deba93.png)

- Using symbolic notation, you can set(=), add(+) or remove(-) permissions for user(u), group(g), other(o)
    - Set: =
    - Add: +
    - Remove: -

- Change the permission of a file: `chmod <perm in any notation> <file>`
    - Eg. `chmod 700 file.txt`
    - Eg. `chmod ugo=rwx file.txt`

- For directories:
    - Read: ls
    - Write: Add/Delete Files
    - Execute cd
 
## Root User
- Highly Privilleged user without any limit
- To execute a command as the root user from a normal user account user `sudo <command>`
- To create a terminal that executes every commaand as the root: `sudo -s` or `su`
- The list of users that can use `sudo` are listed in the `/etc/sudoers` file. To edit the `sudoers` file, use 

### Package Installation
- `apt` is the package manager used on Ubuntu. Do `sudo apt install <pkg>`
- Fetch updates for packages: `sudo apt update`
- Install package updates: `sudo apt upgrade`

### Remote commandline access
- You can access your server remotely over the Secure Shell protocol or ssh. 
- For this an SSH server must already be running on the server on port 22 by default. To install it run `sudo apt install openssh-server``
- After this you can use `ssh <user>@<ip>` from another machine to connect to this

### Transfer files 
1. SFTP: Secure File Transfer Protocol: For multiple tasks -> Gives a dedicated prompt
    - `sftp user@host` -> `get` / `put` / `cd` / `ls` / `help`
2. SCP: Secure Copy - for one-off copying (like `cp`)
    - `scp <from> <to>` Eg. `scp root@10.2.3.5:~/file.txt .` copies the file from the remote systems home folder to the current folder of this system  

## Mounting Drives
- In Linux the drives are mounted on folders 
- After the mounting any files added to the folders is stored in the drive
- Use `df [-h]` to view the mounts with space free, file system type and a lot of other things
- Use `lsblk` to view the mounts
- Use `mount` and `findmnt` for viewing all the mounts including administrative mounts with the paths

![image](https://user-images.githubusercontent.com/54491362/210697842-90e817f3-3a43-4204-82da-d09065464107.png)

The devices are stored in `/dev` folder
