# Foreward
Version 2 of the Zootopia Hit Squad (ZHS2) is a platform to assemble and distribute simple pieces of malware.
Its designed to be used as a teaching tool to perform somewhat sophisticated
attacks in a controlled environment.

Noobs can download pre-written modules, assemble strains based off their
intended purpose, and distribute it without having to write a single line
of code.

# Overview
Bogo is the star of the show. He orchestrates everything, and you'll be interfacing with him.

Users, directories, files, and other "nouns" you want to infect with a payload are called "targets".

Targets are listed in a target file contained within the target directory. See target.d for examples. Targets are basically just a list of names, plus the name of the strain you want to infect those targets with.

A strain is a piece of malware you want Bogo to manage. 

Strains consist of 3 parts:
- a strain file (something.strain), which is simply a configuration file, located in strains.d
- a staging file (something.stage), which are scripts that bogo executes to properly setup or distribute the payload
- the payload itself - which can be several things.
If its really simple, the payload can just be a simple script. It can also be snippets of code that bogo can "assemble" together
into one script. Ideally you want to keep these in a directory, but you don't have to.

Bogo is very flexible with strains. He can work with very sophisticated setups with conditional payloads, or very simple ones.
Prewritten examples are provided in this repository, but I highly encorage that you use them as framework to write your own for your own application.

# Quickstart
- Pull the repo
- (Optional) Change the directory name to "zpd".
If you keep the name "zpd2", change the path ZHS_BASE in global.cfg to reflect this
- Run bogo from the directory. If he has everything he needs, he'll say hes awaiting orders.

# Breakdown: Strains
Bogo interprets the following parameters in a strain file.

He only requires 3 parameters be set: StrainInclude, Payload, and StagingFile. The rest are completly optional, and reserverd for more complex setups.

#### StrainInclude
What files compose the strain? Is it just a single script, or is it multiple?
Put the locations of each file in this array, separated by a space.

#### Payload
What kind of payload is being built? 3 options are supported:

"self" means that what is being built IS the payload, and is intended to be executed by the victim

"none" means there is no payload. What is being built is an executable that Bogo should execute directly.

"external" means the payload is a completely separate file.

#### PayloadLocation
If the Payload parameter is set to External, specify the location of the payload here

#### StagingFile
What is the name of the staging file?
If its a directory, bogo will execute ALL executable files in that directory in alphabetical order.

#### PrestageArgs
Prestaging is a function (or script) that is executed immediately after bogo assembles the strains.

If prestaging is simply a function within a staging file, give the name of the function here so that bogo can pass it
as an argument.
If prestaging is an entire script file, give its name here.

#### StrainAlias
By default, Bogo makes the name of the final executable the name of the strain file.
If you want it to be something different, give its name here.

#### StrainIsSavage
Strains that have the potential to cause some pretty hilarious breakage are labeled "savage".
Bogo will refuse to build savage strains unless BOGO_ALLOW_SAVAGE is set to TRUE in global.cfg

#### ExecuteOnFail
If you want to execute a script in the event infection or staging fails, give its path here.

#### ExecuteOnSuccess
If you want to execute a script in the event infection or staging is successful, give its path here.

#### LaunchTheMissileNow
Set this to true if you want to immediately detonate the payload after its built.
I left this option in for shits and giggles. Bogo will only do it if he is configured to allow savage strains.
