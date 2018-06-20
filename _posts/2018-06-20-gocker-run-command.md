---
layout: post
title: Gocker run command
date: 2018-06-20 21:11 +0000
---


# Main
Setup CLI command instance by using `github.com/urfave/cli`. 


# Main_command
Add two sub-commands into CLI command.
* runCommand: `gocker run`, create container with namespace and cgroups limitation
* initCommand: `gocker init`, internal use only. 


# Run
`runCommand` will call this function.


```mermaid
graph TB
main[Main] -- has --> runCommand(runCommand)
main[Main] -- has --> initCommand(initCommand)


runCommand(runCommand) -- call --> run(Run)

initCommand(initCommand) -- call --> initProcess{RunContainerInitProcess}

run(Run) -- call --> NewParentProcess{NewParentProcess}

NewParentProcess{NewParentProcess} -- exec --> initCommand(initCommand)
```