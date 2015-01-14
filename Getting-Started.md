# Develop Orchard from Source

This is a getting started guide on developing Orchard modules and themes, against the Orchard 
source repository (1.x branch). 

This guide uses TFS as the source control system for 
custom code, however another system would work just as well.

## Prerequesites

This guide uses Git Bash from the [Git for Windows](https://msysgit.github.io/) toolset. Familiarity with command line git and 
the bash shell would help, but will not be necessary.

To make sure you are setup properly, open the Git Bash command line, and change into your working 
directory (paths in Git Bash use the `/` separator character). For example:

>     $ cd /e/working/directory

changes into the Windows directory `E:\working\directory` (you can use upper or 
lower case drive letters).

Now verify that the command `cmd` works. That's right, the Windows command shell - we're going 
to use it too, from within Git Bash! Git Bash should be able to find `cmd.exe`, as it is usually in 
your Windows `%PATH%` (which Git Bash uses to build its `$PATH`). If not, just add it. 

You are ready to begin!

## Getting the Orchard Source

The first step is to get a fresh copy of the Orchard source, currently (Jauary 2015) hosted on 
CodePlex. The project site URL is http://orchard.codeplex.com/, but we're interested in the 
*source code URL*, pointing to the git repository that controls Orchard source. From Git Bash
type the following command:

>     $ git clone https://git01.codeplex.com/orchard OrchardDev

This clones the git repository into the local folder `OrchardDev` inside your working directory. 
Verify that the clone worked by doing the following:

>     $ cd OrchardDev
>     $ git status

You should see output similar to:

>     $ git status
>     On branch master
>     Your branch is up-to-date with 'origin/master'.
>
>     nothing to commit, working directory clean

As stated, we are on the `master` branch - we are viewing the Orchard source code as it exists in 
the `master` branch. This is the release branch, which always contains the source code for the 
most recently released stable version of Orchard (`1.8.1` at the time of writing).

For developing the latest and greatest, we want to checkout (or switch to) the `1.x` branch, the 
active development branch. If you're developing against a different branch (e.g. `1.8.x`) the 
procedure is similar.

>     $ git checkout 1.x

This "switches" branches to `1.x`, and in effect gives us a different view of the files (you'll notice
the messages about downloading changes). Similarly, we can get status information:

>     $ git status
>     On branch 1.x
>     Your branch is up-to-date with 'origin/1.x'.
>
>     nothing to commit, working directory clean

Anytime you want to get the recent changes checked in by the community, simply run:

>     $ git pull origin 1.x

### A bit of indirection

Open up `OrchardDev` in Windows Explorer and you should see Orchard's standard directory layout:

>     /OrchardDev
        /.git
        /lib
        /src
        .gitignore
        other files...
        
Notice the `/.git` subdirectory - this is where git maintains its information on the source code.
For reasons that will become clear later (I promise!), we are going to **move** this `/.git` directory!
Again from Git Bash (and your *working directory*), enter the following commands: 

>     $ mv OrchardDev/.git  ./.git_OrchardDev  
>     $ echo "gitdir: E:/working/directory/.git_OrchardDev" > OrchardDev/.git

Of course, replace `E:/working/directory/` with the path to your 
working directory. 

What we have done is moved the "git tree" to the `.git_OrchardDev` *folder* in our working 
directory, and then created a `.git` *file* inside `OrchardDev` that points git to this *folder*. From
now on, git's tracking data lives in the `.git_OrchardDev` folder, and the source that it is 
tracking lives in the `OrchardDev` folder. Whew!

## Orchard Setup

Orchard makes it pretty easy to setup a new site. Just open the 
`OrchardDev/src/Orchard.sln` in Visual Studio and hit `ctrl+F5` to run the 
`Orchard.Web` project.

**Note:** if you are developing against multiple Orchard instances, you may want to modify the 
*Project Url* in the `Orchard.Web` project to use a different virtual path, before running setup. 
Right-click > Properties > Web, change to your liking (e.g. http://localhost:30321/OrchardDev) 
and then `Create Virtual Directory`.

From the Orchard setup screen: enter your details, choose your storage
mechanism (I like Sql CE for development scenarios), and choose an Orchard setup recipe 
(Core is good for development scenarios; Default is good for quickly getting a site up with some standard content).

In your newly setup Orchard site, enable the `Orchard.CodeGeneration` module (from the Dashboard > Modules). This helps scaffold new 
Module and Theme projects.

## Scaffolding a Module (or Theme)

Now we'll use the Orchard command line to scaffold a new Module project (what follows is similar 
for a theme).

Drop back into Git Bash. We're about to get cross platform! Change into the `Orchard.Web` 
directory (from your *working directory*):

>     $ cd OrchardDev/src/Orchard.Web

and activate `cmd`! It should look similar to:

>     $ cmd
>     Microsoft Windows [Version 6.1.7601]
>     Copyright (c) 2009 Microsoft Corporation.  All rights reserved.
>
>     e:\working\directory\OrchardDev\src\Orchard.Web>

Activating the Orchard command line:

>     e:\working\directory\OrchardDev\src\Orchard.Web> bin\Orchard.exe
>     Initializing Orchard session. (This might take a few seconds...)
>     Type "?" for help, "exit" to exit, "cls" to clear screen
>
>     orchard>

Many Orchard modules define commands that are available from the Orchard command line. 
You can even define your own commands from a custom module!  
The `Orchard.CodeGeneration` module defines the `codegen module` and `codegen theme` 
commands. 

So let's create a module! (for now, we won't include it in the solution).

>     orchard> codegen module NewModule /IncludeInSolution:false
>     Creating Module NewModule
>     Module NewModule created successfully

This creates a folder called `NewModule` inside `E:\working\directory\OrchardDev\src\Orchard.Web\Modules`, and sets up a 
default module structure: the `Module.txt` (module manifest), `NewModule.csproj` and 
`Web.config` files, and some standard folders. 

## Source Controlling the Module

Now that we've scaffolded `NewModule`, we want to place its code under source control. We'll 
use TFS, but git or others would work as well. 

Let's exit out of Orchard's command line program:

>     orchard> exit
>     
>     e:\working\directory\OrchardDev\src\Orchard.Web>

Notice we're still in Windows `cmd` - this is good. We're going to do some more indirection, and 
move our module folder outside of Orchard's source tree. This is to keep Orchard as clean and 
vanilla as possible. Move `NewModule` up into your original *working directory*:

>     e:\working\directory\OrchardDev\src\Orchard.Web> move Modules\NewModule ..\..\..\NewModule\Main

Notice we moved it to `e:\working\directory\NewModule\Main` - the additional `Main` 
folder is for the TFS branch (and so may not be necessary if using git, etc.)

To complete the indirection, create a *folder junction* inside the `Modules` folder, pointing up to the 
new module destination:

>     e:\working\directory\OrchardDev\src\Orchard.Web> mklink /j Modules\NewModule ..\..\..\NewModule\Main

This "tricks" Orchard into believing our Module's soruce is still in the `Modules` folder 
in `Orchard.Web`.

Finally, map `e:\working\directory\NewModule` to a TFS repository/team project. 

## Developing the Module

First things first, you'll need to add the module project to the `Orchard.sln` solution. 

Back in Visual Studio, Right-click the solution > Add > Existing Project. At this point, you'll be shown the file 
browser. **Follow the indirection**, and add the project from within 
`E:\working\directory\OrchardDev\src\Orchard.Web\Modules\NewModule`.  
This is important if/when you need to add references to other Orchard projects/modules from 
within the new module.

Verify everything is all good by launching your Orchard site. In the Dashboard > Modules you should 
be able to find `NewModule` on the list.

From here, development can continue as normal for any other .NET project. For debugging, I find 
the easiest thing to do is

  - start the `Orchard.Web` project normally (start *without* debugging) i.e. `ctrl+F5` 
  - attach to the IISExpress process: `ctrl+alt+p` then find `iisexpress.exe` in the list
  
This allows you to leave the IISExpress site running, and jump into and out of debug mode at any 
time (while taking advantage of Orchard's dynamic compilation features).
