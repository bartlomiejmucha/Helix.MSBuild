# Helix.MSBuild
A small extension for MSBuild that allows to publish Helix solution without Gulp scripts. It's an alternative to https://github.com/richardszalay/helix-publishing-pipeline

It is provided as three standalone files: `Helix.MSBuild.targets`, `Helix.MSBuild.Module.targets` and `Directory.Build.targets`. I provided it in that way (not as a nuget package) so you can easly read and extend the script for your particular needs (and also get familiar with the MSBuild scripts thanks to this).

# Installation
There are only a few steps needed. You can also check out the example solution that is inside `example` folder.

* Create a new `WebRoot` project in your main `src` folder (i.e. where you have `Foundation`, `Feature`, `Project` layers folders). After this step you should have four folders in the `src`.
* Copy the `Helix.MSBuild.targets` and `Helix.MSBuild.Module.targets` files to newly created `WebRoot` project. You can include the files to a `WebRoot` project but in that case set the `Build Action` to `None` for the files as we don't want them to be published as well.
* Open `WebRoot.csproj` and at the end of the file, after all other `<Import>` elements, insert following line: `<Import Project="Helix.MSBuild.targets" />`.
* Copy the `Directory.Build.targets` file to your main `src` folder.
* Install `SlowCheetah` nuget package in `WebRoot` project if you want to apply some transform files during publish.
* Set `<publishUrl>` to actual folder on your disk if you want to apply transform files on a files that are not in your solution.
* Add all module projects you want publish by WebRoot as a project reference in a `WebRoot` project.
* If you want to sync Unicorn with MSBuild check out this extension: https://github.com/bartlomiejmucha/Unicorn.MSBuild

# How it works
The extension allows `WebRoot` project to collect Content files (`Build Action` set to `Content`), Indirect References (that you do not use directly in code, like `Unicorn` nuget package) and Transform files (with `.Helix.` in filename) from all referenced projects. That's why you have to add all your `Foundation`, `Feature` and `Project` projects as a project reference in a `WebRoot`.

The Content files and References are added to publish package and Transform files are applied on files inside publish package before publishing. If you have Remote Transform file (i.e. the file to be transformed is not in the solution), the original file will be copied first from the `<publishUrl>` location to the publish package, then all your Remote Transform files will be applied on that file. The transform files has contains '.Helix.' in the name, for example: `Web.Helix.config`, `Web.Helix.Debug.config`, `Web.Helix.FileSystem.config` (FileSystem is the name of the PublishProfile).
