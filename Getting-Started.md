# Develop Orchard from Source

This is a series of getting started guides on developing Orchard modules and themes, against the Orchard source repository.

These guides use git as the source control system for custom code, however another system would work just as well.

## Prerequesites

These guides use Git Bash from the [Git for Windows](https://msysgit.github.io/) toolset. Familiarity with command line git and the bash shell would help, but will not be necessary.

To make sure you are setup properly, open the Git Bash command line, and change into your working 
directory (paths in Git Bash use the `/` separator character). For example:

    $ cd /e/working/directory

changes into the Windows directory `E:\working\directory` (you can use upper or lower case drive letters).

Now verify that the command `cmd` works. That's right, the Windows command shell - we're going to use it too, from within Git Bash! Git Bash should be able to find `cmd.exe`, as it is usually in your Windows `%PATH%` (which Git Bash uses to build its `$PATH`). If not, just add it. 

## Next Steps

I've broken the next few sections into their own documents. Feel free to follow in sequence, or skip around as needed.

Each section assumes the setup and configuration made in previous sections.

1. [Cloning the Orchard Source](Cloning-Orchard.md)
2. [Scaffolding a Module or Theme](Scaffold-Module-Theme.md)
3. [Source Controlling Custom Code](Source-Control-Custom-Code.md)
4. [Developing and Debugging](Developing-Debugging.md)
