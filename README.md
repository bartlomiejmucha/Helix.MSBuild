# Helix.MSBuild
A small extension for MSBuild that allows to publish Helix solution without Gulp scripts.

# How to use it?
The extension is provided as three standalone files: `Helix.MSBuild.targets` and `Helix.MSBuild.Module.targets` and `Directory.Build.targets`. It is provided that way (not as a nuget package) so you can easly read and extend the script for your needs.
The repository contains an example solution you can check out.
To install it in your solution do the following steps:  
* Create a new WebRoot project in your main source folder (where you have Foundation, Feature, Project layers).
* Copy the `Helix.MSBuild.targets` and `Helix.MSBuild.Module.targets` files to newly created WebRoot project. You can include the files to a WebRoot project but in that case set the `Build Action` to `None` for the files.
* Open `WebRoot.csproj` and at the end of the file, after all other `<Import>` elements, insert following line: `<Import Project="Helix.targets" />`.
* If you want to use transform files, install `SlowCheetah` in `WebRoot` project. Then for each transform file, you have to add this metadata: `<ApplyTransformOnPublish>false</ApplyTransformOnPublish>`.
* If you want to sync Unicorn by MSBuild check out this extension: https://github.com/bartlomiejmucha/Unicorn.MSBuild
* Copy `Directory.Build.targets` file to your main source folder.