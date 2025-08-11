# General Info

Things that I find neat or wish I'd known earlier


- `pwd -P` to avoid symlinks from obscuring the true full path of the current working directory.
- `diff -u file1 file2` for unified diff - great for patches
- `head` shows the first 10 lines of a file.
- Shell variables are not passed to programs that the shell runs. However, Environment variables are. Example:
```sh
FOO=bar # shell variable
export FOO # makes it an environment variable
```
- The order of adding directories to `$PATH` actually matters. The shell looks through the directories in order. This means that, adding your new directory to the beginning of the path makes the shell look in it first.
- `man -k <keyword>` lets you search for a manpage by keyword.
- manpages have [sections](https://man7.org/linux/man-pages/man7/man-pages.7.html). `ping(8)` <- `8` is from the section `System commands and servers`. I finally know what the numbers mean :)
- Redirect standard output and error using `command > file 2>&1`
- Useful `ps` flags:
```sh
ps u # more info
ps w # show full command, no truncation
ps x # all of my running processes
ps ax # all running processes, not just mine
```
- `kill -l` shows mapping of signal numbers to names.
- `jobs` command shows any suspended processes.
- `nohup` allows processes to live when the terminal gets killed.
- Useful absolute permission modes:

| Mode | Used for              | User | Group | Other |
|------|-----------------------|------|-------|-------|
| 644  | files                 | rw   | r     | r     |
| 600  | files                 | rw   | -     | -     |
| 755  | directories, programs | rwx  | rx    | rx    |
| 700  | directories, programs | rwx  | -     | -     |
| 711  | directories           | rwx  | x     | x     |

  - Note how the directories are being given execute permissions. This is because you can list the contents of the file, if it is readable, but you can only access a file in a directory, if the directory is executable.

- The kernel is generally a binary file `/vmlinuz` or `/boot/vmlinuz`. The boot-loader loads this during system boot. However, `/lib/modules` contain modules called `loadable kernel modules` that the kernel loads and unloads on demand.
 

