# C-shell

A simple Unix shell written in C, built as a personal learning project by following Stephen Brennan's tutorial [Write a Shell in C](https://brennan.io/2015/01/16/write-a-shell-in-c/).

> Work in progress: the shell is being built step by step as I go through the tutorial.

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
gcc -o shell shell.c
./shell
```

## What I'm learning

- How a shell's lifecycle works (initialize, interpret, terminate)
- Dynamic memory allocation for reading input of unknown length
- Tokenizing strings with `strtok`
- Process creation and management with `fork`, `exec` and `wait`
- How built-in commands differ from external programs

## Credits

Based on [Write a Shell in C](https://brennan.io/2015/01/16/write-a-shell-in-c/) by Stephen Brennan.
