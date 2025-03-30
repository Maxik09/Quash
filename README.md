# Quite a Shell (Quash) - Custom Unix Shell

This project is a custom-built Unix shell implemented in C, developed as part of an academic assignment focused on understanding core concepts of operating systems and Unix internals. The goal was to simulate a Bash-like experience with support for process control, I/O redirection, piping, and environment management using system calls.

---

## 🚀 Features Implemented

### ✅ Core Shell Execution
- Executables run via absolute/relative path or via `$PATH`
- Foreground and background job execution (`&` support)
- Clear job start and completion messages

```bash
[QUASH]$ ./long_task &
Background job started: [1] 2342 ./long_task &
[QUASH]$ echo done
Completed: [1] 2342 ./long_task &
```

### ✅ Built-in Commands
- `echo` - Prints arguments and supports environment variable substitution.
- `export` - Sets environment variables.
- `cd` - Changes current working directory and updates `PWD`.
- `pwd` - Prints the actual working directory (not just `PWD`).
- `jobs` - Lists background jobs with their IDs, PIDs, and commands.
- `quit` and `exit` - Properly exit the shell.

### ✅ Process Management
- Robust job tracking with unique job IDs
- Maintains job lists using a deque data structure (from `src/deque.h`)
- Background job completion detection and output

### ✅ I/O Redirection
- `>` - Truncates and writes to file
- `>>` - Appends to file
- `<` - Redirects input from file
- Handles multiple redirection operations per command

### ✅ Piping
- Pipe (`|`) support between multiple commands
- Mixed piping and redirection
- Example:

```bash
cat file.txt | grep Hello | tee output.txt
```

---

## 🧠 Learning Objectives
- Understand and implement process control using `fork()`, `execvp()`, and `waitpid()`
- Manipulate file descriptors using `dup2()` for redirection and piping
- Use `chdir()`, `setenv()`, and `getenv()` to manage the working directory and environment variables
- Monitor and manage multiple child processes in background jobs

---

## 🛠️ Technical Highlights

- Modularized design in `src/execute.c` for command execution logic
- Parsing handled separately in `src/parsing/`
- Usage of custom deque macros for job management
- System calls used:
  - `fork`, `execvp`, `dup2`, `pipe`, `waitpid`, `chdir`, `open`, `kill`, `getenv`, `setenv`, `exit`
- Built-in command implementations are run without `exec`
- Complete valgrind-clean memory management (no leaks)

---

## 🧪 Testing
- Comprehensive test suite with `run_tests.bash`
- Supports output diff checks and memory error validation
- Run via `make test` or manually with flags (e.g., `-v` for verbose)

---

## 📦 Build & Run
```bash
# Build the shell
make

# Run Quash
./quash

# Clean build
make clean

# Generate documentation
make doc
```

---

## 💡 Project Structure
```
quash/
├── src/
│   ├── execute.c        # Core logic for command execution
│   ├── deque.h          # Custom double-ended queue macros
│   └── parsing/         # Provided parser utilities (not modified)
├── run_tests.bash       # Test automation script
├── Makefile             # Build & test rules
└── README.md            # Project summary and usage
```


---

## 🧼 Memory Safety
- Zero valgrind errors
- All dynamically allocated memory is freed properly
- No use-after-free, invalid reads/writes, or uninitialized access

---

## 🔐 Constraints Followed
- No use of `system()` function
- Parsing code left unmodified (except `destroy_parser()`)
- Matches output format strictly per specification

---

## 📁 Submission Format
- Uses `make submit` to package code with `.txt` extensions for submission
- Validated using `make unsubmit` to ensure no build errors

---

## 🤝 Collaboration
Project completed in a team of 2, collaborating on:
- I/O redirection and pipes logic
- Background job manager
- Command execution loop
- Test case debugging and memory cleanup

---

## 📌 Summary
This project simulates a functional Unix shell with realistic command execution behavior. It allowed me to dive deep into system-level programming, learning how shells work under the hood, and how to build robust and extensible software using low-level tools. Perfect for developers interested in OS, systems programming, and process control.

---



