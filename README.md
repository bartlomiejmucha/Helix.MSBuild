# Helix.MSBuild
A small extension for MSBuild that allows to publish Helix solution without Gulp scripts.

It is provided as three standalone files: `Helix.MSBuild.targets`, `Helix.MSBuild.Module.targets` and `Directory.Build.targets`. I provided it in that way (not as a nuget package) so you can easly read and extend the script for your particular needs (and also get familiar with the MSBuild thanks to this).

# Installation
There are only a few steps needed. You can also check out the example solution that is inside `example` folder.

* Create a new new `WebRoot` project in your main `src` folder (i.e. where you have `Foundation`, `Feature`, `Project` layers folders). After this step you should have four folders in the `src`.
* Copy the `Helix.MSBuild.targets` and `Helix.MSBuild.Module.targets` files to newly created `WebRoot` project. You can include the files to a `WebRoot` project but in that case set the `Build Action` to `None` for the files.
* Open `WebRoot.csproj` and at the end of the file, after all other `<Import>` elements, insert following line: `<Import Project="Helix.MSBuild.targets" />`.
* If you want to use transform files, install `SlowCheetah` in `WebRoot` project. Then for each transform file, you have to add this metadata: `<ApplyTransformOnPublish>true</ApplyTransformOnPublish>`. Check out the example solution for more details.
* Copy the `Directory.Build.targets` file to your main `src` folder.
* If you want to sync Unicorn with MSBuild check out this extension: https://github.com/bartlomiejmucha/Unicorn.MSBuild
