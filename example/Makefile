
include ../Makefile

# Run commands with the node debugger. (default: false)
DEBUG ?= false

ifeq ($(DEBUG),false)
	node = node
else
	node = node debug
endif

# Remove all the installed and compiled files.
clean:
	@ rm -rf ./node_modules ./lib

# Compile the source files with Babel.
lib:
	@ ./node_modules/.bin/babel-cli --out-dir ./lib ./src

# Start the development server.
start:
	@ $(node) ./server/index.js
