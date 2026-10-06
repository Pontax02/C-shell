# C-shell

A simple Unix shell written in C, built as a personal learning project by following Stephen Brennan's tutorial [Write a Shell in C](https://brennan.io/2015/01/16/write-a-shell-in-c/).

The shell implements every part of the tutorial and builds and runs under Linux or WSL.

## What it does

The shell runs a basic **read → parse → execute** loop:

1. **Read** a line of input from the user.
2. **Parse** the line into a program name and arguments, splitting on whitespace.
3. **Execute** the command, either as a built-in or by launching a new process.

### Built-in commands

| Command | Description |
| --- | --- |
| `cd <dir>` | Change the current directory |
| `help` | Show help and the list of built-ins |
| `exit` | Exit the shell |

Any other command is run as a program using `fork()`, `execvp()` and `waitpid()`.

## Limitations

Like the tutorial's shell, this one is kept simple on purpose:

- Arguments are split on whitespace only, with no quoting or backslash escaping
- No piping (`|`) or redirection (`>`, `<`)
- Only a few built-ins
- No globbing or environment variable expansion

## Building and running

The shell uses POSIX system calls such as `fork` and `execvp`, so it needs a Unix-like environment (Linux, macOS, or WSL on Windows).

```sh
gcc -Wall -o shell shell.c
./shell
```

### On Windows

Build and run inside WSL. Windows compilers such as MinGW don't provide `sys/wait.h` or `unistd.h`. For the same reason, an editor using a Windows compiler will report "cannot open source file" errors on those includes, even though the code is correct.

```sh
sudo apt install gcc        # first time only
cd /mnt/c/path/to/C-shell
gcc -Wall -o shell shell.c
./shell
```

## What I'm learning

- How a shell's lifecycle works (initialize, interpret, terminate)
- Dynamic memory allocation for reading input of unknown length
- Tokenizing strings with `strtok`
- Process creation and management with `fork`, `exec` and `wait`
- How built-in commands differ from external programs
- Why to flush `stdout` before `fork()`: the child gets a copy of any unwritten output and prints it again when it exits

## Credits

Based on [Write a Shell in C](https://brennan.io/2015/01/16/write-a-shell-in-c/) by Stephen Brennan.
