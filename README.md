# Foreward
Version 2 of the Zootopia Hit Squad (ZHS2) is a platform to assemble and distribute simple pieces of malware.
Its designed to be used as a teaching tool to perform somewhat sophisticated
attacks in a controlled environment.

Noobs can download pre-written modules, assemble strains based off their
intended purpose, and distribute it without having to write a single line
of code.

# Overview
Bogo is the star of the show. He orchestrates everything, and you'll be primarily interfacing with him.

Users, directories, files, and other "nouns" you want to infect with a payload are called "targets"
Targets are listed in a target file contained within the target directory. See target.d for examples.
Basically its just a list of names, plus the name of the strain you want to infect those targets with.

A strain is a piece of malware you want Bogo to manage. 

Strains consist of 3 parts:
- a strain file (something.strain), which acts as a configuration file, located in strains.d
- a staging file (something.stage), which are scripts that bogo executes to properly setup or distribute the payload
- the payload itself - which can be several things.
If its really simple, the payload can just be a simple script. It can also be snippets of code that bogo can "assemble" together
into one script. Ideally you want to keep these in a directory, but you don't have to.

Bogo is very flexible with strains. He can work with very sophisticated setups with conditional payloads, or very simple ones.
Prewritten examples are provided in this repository, but I highly encorage that you use them as framework to write your own for your own application.

# Quickstart
