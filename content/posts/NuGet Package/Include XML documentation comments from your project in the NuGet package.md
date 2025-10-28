---
title: Add XML Docs to NuGet
date: '2025-10-28T10:06:50+08:00'
tags:
  - dotnet
  - nuget
categories:
  - nuget-package
---
## Step 1: Enable XML Documentation Generation

1. In your project, right-click and select "Properties".
2. In the project properties window, go to the "Build" tab.
3. Check the "XML documentation file" checkbox and optionally provide a file path for the XML file. If left blank, it will generate the file in the output directory.

## Step 2: Build the Project

Build your Utility project to generate the XML documentation file.

## Step 3: Create the NuGet Package

1. Open a command prompt or PowerShell window and navigate to your Utility project directory.
2. Run the following command to create the NuGet package, which will include the XML documentation file:
```bash
dotnet pack --configuration Release
```