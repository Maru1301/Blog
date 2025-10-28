---
title: Create a NuGet Package Guide
date: '2025-10-28T10:06:51+08:00'
tags:
  - dotnet
  - nuget
---


1. **Project Structure:** Ensure your project structure follows the NuGet conventions. Specifically, the assemblies should be placed in the lib folder within your package.
```xml
YourProject 
├── lib 
│   └── net8.0 
│       └── <Your Project>.dll 
├── docs 
│   └── README.md 
├── contentFiles 
│   └── any 
│       └── any 
│           └── somefile.txt (optional) 
├── tools 
│   └── someTool.exe (optional) 
├── build 
│   └── net8.0 
│       └── <Your Project>.targets (optional) 
└── <Your Project>.nuspec
```
1. **.nuspec File:** Ensure your .nuspec file is correctly configured to include the necessary files. Here’s an example .nuspec file:
```XML
<?xml version="1.0"?> 
<package > 
	<metadata> 
		<id>YourLibrary</id> 
		<version>1.0.0</version> 
		<authors>YourName</authors> 
		<owners>YourName</owners> 
		<readme>docs\README.md</readme> 
		<description>Your library description</description> 
		<tags>tag</tags> 
		<dependencies> 
			<group targetFramework=".NET8.0"> 
				<dependency id="dependency" version="1.0.0" /> 
			</group> 
		</dependencies> 
	</metadata> 
	<files> 
		<file src="lib\net8.0\<Your Project>.dll" target="lib\net8.0\" />     
		<file src="..\README.md" target="docs\" /> 
		<!-- Add other necessary files here --> 
	</files> 
</package>
```
    
2. **Building the NuGet Package:** Use the nuget pack command to create the NuGet package. Make sure your project is built and the necessary files are in place before packing.
```shell
nuget pack YourProject.nuspec
```
    
3. **Automating with .csproj:** Alternatively, you can use the .csproj file to automate the creation of the NuGet package. This approach leverages the dotnet pack command. Here’s an example of how to configure your .csproj file:
```XML
<Project Sdk="Microsoft.NET.Sdk"> 
	<PropertyGroup> 
		<TargetFramework>net8.0</TargetFramework> 
		<GeneratePackageOnBuild>true</GeneratePackageOnBuild> 
		<PackageId>YourLibrary</PackageId> <Version>1.0.0</Version> 
		<Authors>YourName</Authors> 
		<PackageReadmeFile>README.md</PackageReadmeFile> 
		<Description>Your library description</Description> 
	</PropertyGroup> 
	<ItemGroup> 
		<None Include="docs\README.md" Pack="true" PackagePath="\"/> 
	</ItemGroup> 
</Project>
```
    
4. **Release with NuGet Package:**
```shell
dotnet pack -c Release -o obj\Release\Nuget\
```
    
5. **Advanced(optional):**
	[[Include XML documentation comments from your project in the NuGet package]]
	[[Use GitHub Actions to publish a NuGet package to GitHub Packages]]
## Additional

### 'nuget' is not recognized

To resolve the error where 'nuget' is not recognized as a command:

- Download nuget.exe from the official NuGet website.
- Add the directory containing nuget.exe to your system's PATH environment variable.

### Warning NU5128

To address the NU5128 warning in NuGet, follow these steps:

1. **Check Your Project Target Framework**  
    Ensure the project’s target framework is correctly specified in your .csproj or project settings (e.g., .NET 8.0).
    
2. **Update the .nuspec File**  
    Modify your .nuspec file to include dependencies specific to the target framework. Below is an example:
```XML
<?xml version="1.0" encoding="utf-8"?>
<package>
<metadata>
	<!-- Other metadata elements -->
	<dependencies>
		<group targetFramework="net8.0">
			<dependency id="SomeDependency" version="1.0.0" />
		</group>
	</dependencies>
	<!-- Other metadata elements -->
</metadata>
</package>
```
3. **Ensure Proper Folder Structure**  
The package directory structure must align with the target framework. Place your DLLs in the appropriate lib folder as shown below:
```xml
YourProject 
├── lib 
│   └── net8.0 
│       └── Utility.dll 
├── docs 
│   └── README.md 
└── YourProject.nuspec
```