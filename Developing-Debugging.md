# Developing and Debugging

Firstly, you'll need to add the Module (Theme) project(s) to the `Orchard.sln` solution. 

Back in Visual Studio, Right-click the solution > Add > Existing Project. At this point, you'll be shown the file 
browser. **Follow the indirection** that was setup earlier, and add the project from within 
`E:\working\directory\OrchardDev\src\Orchard.Web\Modules\NewModule`.  

e.g. we don't add the project from it's **actual location** on disk, but rather from the **junction location**.

This is important for maintaining project references to other Orchard projects/modules from 
within the new module.

Verify everything is all good by launching your Orchard site. In the Dashboard > Modules you should be able to find `NewModule` on the list.

From here, development can continue as normal for any other .NET project. For debugging, I find the easiest thing to do is

  - start the `Orchard.Web` project normally (start *without* debugging) i.e. `ctrl+F5` 
  - attach to the IISExpress process: `ctrl+alt+p` then find `iisexpress.exe` in the list
  
This allows you to leave the IISExpress site running, and jump into and out of debug mode at any 
time (while taking advantage of Orchard's dynamic compilation features).