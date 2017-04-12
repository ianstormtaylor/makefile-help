
# makefile-help

An easy way to add a `make help` target to your Makefiles, that is auto-populated from comment lines above your make targets.

---

### Example

For a makefile like...

```make
ifneq ($(wildcard ./node_modules),)
  include ./lib/modules/makefile-help/Makefile
  include ./lib/modules/makefile-assert/Makefile
endif

# Run commands with the node debugger. (default: false)
DEBUG ?= false

ifeq ($(DEBUG),false)
  node = node
else
  node = node debug
endif

# Remove all of the derived files.
clean: 
  @ rm -rf ./node_modules ./lib

# Compile the source with babel.
lib: 
  @ ./node_modules/.bin/babel-cli --out-dir ./lib ./src

# Start the development server.
start:
  @ $(node) ./server/index.js
```

Running `make help` will print out...

```bash
$ make help

  Usage:

    make <target> [flags...]

  Targets:

    clean   Remove all of the derived files.
    help    Show this help prompt.
    lib     Compile the source with babel.
    start   Start the development server.

  Flags:

    DEBUG    Run commands with the node debugger. (default: false)

```

---

### Installation

```bash
npm install --save makefile-help
```

---

### Usage

To use it, `include` this module's `Makefile` in your own...

```make
ifneq ($(wildcard ./node_modules),)
  include ./node_modules/makefile-help/Makefile
endif
```

And then run...

```bash
$ make help
```

The help command will auto-populate from targets that look like:

```make
# This comment will show up for the target in the help.
target:
```

And also for flag definitions like:

```make
# This comment will show up for the flag in the help.
FLAG ?= false
```
