# Gorilla Tag Stripped Assemblies [![Generate Stripped DLLs](https://github.com/sirkingbinx/gtci/actions/workflows/generate.yml/badge.svg)](https://github.com/sirkingbinx/gtci/actions/workflows/generate.yml)
This is mostly meant for building mods on Actions runners without any access to a Gorilla Tag installation. This fully strips the assemblies so you aren't breaking the LAW when downloading assemblies over the internet.

[This composite GitHub action](https://github.com/sirkingbinx/setup-gorilla-tag) will automatically do the hard labor of setting up Gorilla Tag and BepInEx, just point your project to the Libs folder when building over actions.

```yml
name: Build Mod

on:
  push:
    branches: [ master ]
  workflow_dispatch:

jobs:
  build:
    runs-on: windows-latest
    steps:
      - name: Checkout Repository
        uses: actions/checkout@v4

      - name: Setup MSBuild
        uses: microsoft/setup-msbuild@v2
  
      - name: Setup NuGet
        uses: NuGet/setup-nuget@v1

      - name: Setup Gorilla Tag
        uses: sirkingbinx/setup-gorilla-tag@1.0.0

      - name: Build Solution
        run: |
          dotnet build -c Debug
          dotnet build -c Release
```

These assemblies can be downloaded from anywhere, so you're free to setup Gitea Actions or whatever else you want with these assemblies.
