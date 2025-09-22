# Getting started with Linux Command Line using Argon
In this page, the essential Linux commands are listed. You can exercise all commands below on the Argon cluster.


## First helpers

!!! note "man [option] [section number] [command name]"

    display a comprehensive guide of commands.
    If no section number, it will print out the entire manual of the requested command.

!!! note "history [option]"

    check previous run utilities

    ```bash

    dooyoon@argon-itf-login-3 ~> history
    1  cd
    2  ls
    ```
---

## Navigation

!!! note "pwd [option]"

    print current working directory's path

    - -L (--logical)
    - -P (--physical)


!!! note "ls [option] [/directory/folder/path]"

    list files and directories in your system

    Options

    - -a: show hidden content
    - -R: list items inside subfolders
    - -h: print file sizes in human-readable format
    - -F: type of objects  /: directory, @: link, \*: executable
    - -l: display detailed information 

    ``` bash

     dooyoon@argon-itf-login-4 ~> ls -altrh
     total 4.5M
     -rw-r--r--  1 dooyoon 5.4K Dec  7  2023 .vimrc
     drwxr-xr-x  2 dooyoon    5 Dec  7  2023 .vim-file
     lrwxrwxrwx  1 dooyoon   26 Feb 19  2024 nfsscratch -> /nfsscratch/Users/dooyoon/
     drwx------  3 dooyoon    3 Feb 28  2024 .dbus
     -rw-------  1 dooyoon   16 Feb 28  2024 .esd_auth
     drwxr-xr-x  2 dooyoon    2 Feb 28  2024 Desktop
     drwxr-xr-x  2 dooyoon    2 Feb 28  2024 Downloads
     drwxr-xr-x  2 dooyoon    2 Feb 28  2024 Templates
    ```
    
!!! note "cd [/directory/folder/path]"

    move to the destination folder

    - **Absolute path**: start w/ the root directory and provide the full path to the file or directory
    - **Relative path**: a path to a file or directory that is relative to the current directory  

---


File/Directory Manipulation
---------------------------

!!! note "mkdir [directory name]"

    create one or multiple directories

!!! note " cp [option] [source object] [target path or file name]"

    copy files or directories to another file names or target ath

    Options 

    - -R: all sub-directory
    - -f: force to copy
    - -v: verbose

!!! note "mv [source object] [target path or file name]"

    move files or directories to a new location or rename them


!!! note "rm [option] [file names or directory names]"
   
    remove files or directories

    Options 

    - -i: prompt a confirmation before deletion
    - -f: allow file removal without confirmation
    - -r: delete files and directories recursively

    !!! warning

        In most cases, deleted files and directories cannot be recovered. 


!!! note "touch [option] [file name]"

    create a new empty file in a specific directory


!!! note "cat [file name]"

    print the content of a text file

    !!! info

        You can also use `cat` with the operator to combine multiple files into a new file. 
   
        ```bash

        dooyoon@argon-itf-login-4 ~> cat file1.txt file2.txt > target_file.txt
        ```

!!! note "head [option] [file name]"

    print the first few entries of a file 

    Options

    - -n: number of lines

!!! note "tail [option] [file name]"

    print the last few entries of a file

    Options 

    - -n: number of lines
    - **-f: output appended the data (i.e., display the lines in real time)**


!!! note "grep [option] keyword [file name]"

    search specific lines from a file using keyword 
    -> Useful for filtering large data like logs


!!! note "ln [option] [source] [destination]"

    create links between files or directories

    - hard link:
        - only files on a same partition
        - link to inode
    - symbolic link:
        - option: `-s`
        - point to files or directories
        - considered as "shortcuts"

    ```bash

    dooyoon@argon-itf-login-4 links_hard_symbolic> ls -il *
      285698 -rw-r--r-- 2 dooyoon 4 Sep  3 15:33 source1
      285698 -rw-r--r-- 2 dooyoon 4 Sep  3 15:33 source1-hard
      285699 -rw-r--r-- 1 dooyoon 4 Sep  3 15:22 source2
      285701 lrwxrwxrwx 1 dooyoon 7 Sep  3 15:30 source2-soft -> source2
    ```

!!! note "which [command]"

    search for executable **First** commands in the PATH environment

!!! note "whereis [option] [command]"

    display the path of the binary source, and manual page files in the PATH or MANPATH environment

!!! note "locate [option] [command]"

    search all files that include pattern in the pre-existed database

!!! note "find [dir] [option] [expression]"

    search files and directories in any designated directory

!!! note "chmod [option] [permission] [file or directory]"

    change permission of files or directories

    - u: user / g: group / o: other / a: all
    - r: read / w: write / x: execute

    ```bash

    dooyoon@argon-itf-login-4 Executable> ls -l
      -rwxr--r-- 1 dooyoon 38 Sep  5 14:08 hello.sh

    dooyoon@argon-itf-login-4 Executable> chmod ugo+x hello.sh
    dooyoon@argon-itf-login-4 Executable> ls -l
      -rwxr-xr-x 1 dooyoon 38 Sep  5 14:08 hello.sh
    ```

    - Octal Number: r=4 / w=2 / x=1

    ```bash

    dooyoon@argon-itf-login-4 Executable> chmod 755 hello.sh
    dooyoon@argon-itf-login-4 Executable> ls -l
      -rwxr-xr-x 1 dooyoon 38 Sep  5 14:08 hello.sh
    ```

!!! note "df [option] [file system]"

    check your system's disk usage

    Options 

    - -h: print file sizes in human-readable format

    ```bash

    dooyoon@argon-itf-login-3 ~> df -h $HOME
      Filesystem                          Size  Used Avail Use% Mounted on
      172.29.4.38:/dpool01/Homes/dooyoon  1.0T   20G 1005G   2% /old_Users/dooyoon
    ```

!!! note "du [option] [directory]"

    check the size of a directory and its content

    Options 

    - -h: print file sizes in human-readable format
    - -d, --max-depth=N: print the total for a directory only if it is N or fewer levels below.  


---

## Archive & Unpack targets

!!! note "tar [option] [archive file] [target objects]"

    bundle multiple files or directories into an archive

    Options 

    - c or x: create or extract
    - v     : verbose
    - f     : specify the archive file
    - z or j: compression (file extension -> .tar.gz or .tar.bz2) 
            without compression, the extension will be .tar

!!! note "zip [option] [archive file] [target objects]"

    bundle and compress multiple files or directories using zip

!!! note "unzip [option] [archive file]"

    extract the zip archived file

---

## File Transfer

!!! note "wget [option] [URL]"

    download files from the internet via HTTP, HTTPS, or FTP protocols

!!! note "curl [option] [URL]"

    transfer data from or to a server by specifying its URL

    Options

    - -O/-o: download files from the specific link

!!! note "scp [option] [source] [address]:[destination folder]"
 
    securely copy files and directories between systems over a network

!!! note "rsync [option] [source] [address]:[destination folder]"

    syncs files or directories between two destinations to ensure they have the same content

    Options 

    - -r: recurse into sub-directories
    - -a: archive mode, keeps all file permissions, symbolic links,file ownership, etc
    - **-u: skip files that are newer on the receiver**
