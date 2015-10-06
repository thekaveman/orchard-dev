# Source Controlling Custom Code

There are number of different approaches for organizing custom code (Modules and Themes) within a local Orchard source repo.

What follows is a setup that has *worked for me* in various projects, with small numbers of custom modules/themes. In practice, the setup process could largely be scripted (powershell, bash, etc), for more complex scenarios.

The result is: your code is kept entirely separate and independent of the Orchard source, and Modules (and Themes) can be reused across projects *as source code* (if that's your thing).

## Working with a Scaffolded Module (Theme)

> This assumes you have just scaffolded a module `NewModule` using the Orchard command line program. 

Exit out of Orchard's command line program (if you're still in it):

    orchard> exit
    
    e:\working\directory\OrchardDev\src\Orchard.Web>

Move `NewModule` up into your original *working directory*:

    e:\working\directory\OrchardDev\src\Orchard.Web> move Modules\NewModule ..\..\..\NewModule

To complete the indirection, create a *folder junction* inside the `Modules` folder, pointing up to the 
new module destination:

    e:\working\directory\OrchardDev\src\Orchard.Web> mklink /j Modules\NewModule ..\..\..\NewModule

Verify by opening Windows Explorer to the `Modules` folder; you should see what looks like a shortcut to `NewModule`.

### Control Yourself

Finally, you can create a git repository for the Module back inside the **physical** location

    e:\working\directory\OrchardDev\src\Orchard.Web> cd ..\..\..\NewModule
    e:\working\directory\NewModule> git init
    
## Working with a Cloned Module (Theme)

> This assumes you have cloned a module `ClonedModule` into your working directory `e:\working\directory\ClonedModule`
> and that you have an Orchard source installation `OurchardDev` in the same working directory `e:\working\directory\OrchardDev`

Start up `cmd` (either from within Git Bash or standard `cmd`) and change into the working directory. The process here will be similar to above:

Create a *folder junction* inside the `Modules` folder in `OrchardDev`, pointing up to the cloned module destination:

    e:\working\directory> cd OrchardDev\src\Orchard.Web
    e:\working\directory\OrchardDev\src\Orchard.Web> mklink /j Modules\ClonedModule ..\..\..\ClonedModule
    
Again, verify by opening Windows Explorer to the Modules folder; you should see what looks like a shortcut to ClonedModule.