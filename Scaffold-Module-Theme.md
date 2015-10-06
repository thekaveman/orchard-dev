# Scaffolding a Module or Theme

## Orchard Setup

Orchard makes it pretty easy to setup a new site. Just open the 
`OrchardDev/src/Orchard.sln` in Visual Studio and hit `ctrl+F5` to run the 
`Orchard.Web` project.

> **Note:** if you are developing against multiple Orchard instances, you may want to modify the *Project Url* in the `Orchard.Web` project to use a different virtual path, before running setup. 
> 
> Right-click > Properties > Web, change to your liking (e.g. http://localhost:30321/OrchardDev) 
and then `Create Virtual Directory`.

From the Orchard setup screen: enter your details, choose your storage
mechanism (I like Sql CE for development scenarios), and choose an Orchard setup recipe 
(`core` is good for development scenarios; `default` is good for quickly getting a site up with some standard content).

In your newly setup Orchard site, enable the `Orchard.CodeGeneration` module (from the Dashboard > Modules). This helps scaffold new 
Module and Theme projects.

## Scaffolding a Module (or Theme)

Now we'll use the Orchard command line to scaffold a new Module project (what follows is similar for a theme).

Drop back into Git Bash. We're about to get cross platform! Change into the `Orchard.Web` 
directory (from your *working directory*):

    $ cd OrchardDev/src/Orchard.Web

and activate `cmd`! It should look similar to:

    $ cmd
    Microsoft Windows [Version 6.1.7601]
    Copyright (c) 2009 Microsoft Corporation.  All rights reserved.
    
    e:\working\directory\OrchardDev\src\Orchard.Web>

Activating the Orchard command line:

    e:\working\directory\OrchardDev\src\Orchard.Web> bin\Orchard.exe
    Initializing Orchard session. (This might take a few seconds...)
    Type "?" for help, "exit" to exit, "cls" to clear screen
    
    orchard>

Many Orchard modules define commands that are available from the Orchard command line. 
You can even define your own commands from a custom module!  
The `Orchard.CodeGeneration` module defines the `codegen module` and `codegen theme` 
commands. 

So let's create a module! (for now, we won't include it in the solution).

    orchard> codegen module NewModule /IncludeInSolution:false
    Creating Module NewModule
    Module NewModule created successfully

This creates a folder called `NewModule` inside `E:\working\directory\OrchardDev\src\Orchard.Web\Modules`, and sets up a 
default module structure: the `Module.txt` (module manifest), `NewModule.csproj` and 
`Web.config` files, and some standard folders.