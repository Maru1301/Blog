---
title: Publish NuGet to GitHub Packages with Actions
date: '2025-10-28T10:06:52+08:00'
tags:
  - dotnet
  - github
  - nuget
---

### 1. **Prepare Your Project**

Ensure that your project includes:

- A `.csproj` or `.nuspec` file with proper metadata.
- The `PackageId`, `Version`, and other relevant fields filled in the `.csproj` file or `.nuspec`.
```xml
<PropertyGroup>
  <PackageId>YourPackageName</PackageId>
  <Version>1.0.0</Version>
  <Authors>YourName</Authors>
  <Description>Your package description</Description>
  <RepositoryUrl>https://github.com/<OWNER>/<REPO></RepositoryUrl>
</PropertyGroup>
```

---

### 2. **Set Up a GitHub Personal Access Token (PAT)**

1. Go to your GitHub account settings.
2. Navigate to **Developer settings** > **Personal access tokens** > **Tokens (classic)**.
3. Generate a token with the `write:packages` and `read:packages` permissions.
4. Add this token as a secret in your repository:
    - Go to your repository’s **Settings** > **Secrets and variables** > **Actions** > **New repository secret**.
    - Name the secret something like `GH_PACKAGES_TOKEN`.

---

### 3. **Create a GitHub Actions Workflow**

Create a `.yml` file in the `.github/workflows` directory of your repository. For example, create `.github/workflows/publish-nuget.yml`:
```yaml
name: Publish NuGet Package

on:
  push:
    tags:
      - 'v*.*.*' # Trigger on version tags (e.g., v1.0.0)

jobs:
  publish:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout repository
      uses: actions/checkout@v3

    - name: Set up .NET
      uses: actions/setup-dotnet@v3
      with:
        dotnet-version: '8.x' # Adjust according to your project

    - name: Restore dependencies
      run: dotnet restore

    - name: Build the project
      run: dotnet build --configuration Release --no-restore

    - name: Pack the NuGet package
      run: dotnet pack --configuration Release --no-build --output ./output

    - name: Publish to GitHub Packages
      run: dotnet nuget push ./output/*.nupkg --api-key ${{ secrets.GH_PACKAGES_TOKEN }} --source "https://nuget.pkg.github.com/<OWNER>/index.json"
      env:
        GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}

```
---
### 4. **Key Points in Workflow**

- **Trigger**: The workflow triggers on `push` events with tags following a semantic versioning pattern (e.g., `v1.0.0`).
- **Dotnet CLI Commands**:
    - `dotnet restore`: Restores project dependencies.
    - `dotnet build`: Builds the project.
    - `dotnet pack`: Creates the `.nupkg` file.
    - `dotnet nuget push`: Publishes the package.
- **Source URL**: Replace `<OWNER>` in `https://nuget.pkg.github.com/<OWNER>/index.json` with your GitHub username or organization name.

---

### 5. **Push and Tag Your Release**

1. Commit and push your changes.
2. Create a new tag:
```bash
  git tag v1.0.0
  git push origin v1.0.0
```