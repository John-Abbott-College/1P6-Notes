# Running your C# program on a MAC



[reference](https://www.reddit.com/r/csharp/comments/9obuj9/where_is_the_executable_file_not_necessarily_exe/)

## Tree structure 

Note that the directory that I am in is the `project` directory, and not the `solution` directory.

```bash
[~/Projects/HelloWorld/HelloWorld] tree
.
├── HelloWorld.csproj
├── Program.cs
├── bin
│   └── Debug
│       └── netcoreapp2.1
│           ├── HelloWorld.deps.json
│           ├── HelloWorld.dll
│           ├── HelloWorld.pdb
│           ├── HelloWorld.runtimeconfig.dev.json
│           └── HelloWorld.runtimeconfig.json
└── obj
    ├── Debug
    │   └── netcoreapp2.1
    │       ├── HelloWorld.AssemblyInfo.cs
    │       ├── HelloWorld.AssemblyInfoInputs.cache
    │       ├── HelloWorld.assets.cache
    │       ├── HelloWorld.csproj.CoreCompileInputs.cache
    │       ├── HelloWorld.csproj.FileListAbsolute.txt
    │       ├── HelloWorld.csprojAssemblyReference.cache
    │       ├── HelloWorld.dll
    │       └── HelloWorld.pdb
    ├── HelloWorld.csproj.nuget.cache
    ├── HelloWorld.csproj.nuget.dgspec.json
    ├── HelloWorld.csproj.nuget.g.props
    ├── HelloWorld.csproj.nuget.g.targets
    ├── project.assets.json
    └── project.nuget.cache

6 directories, 21 files
```

## Running the code
Note that I have to be in the project directory for this to work, and I have to have visual studio installed.

```bash
[~/Projects/HelloWorld/HelloWorld] dotnet run
Hello World!
```

## Publishing the code 

To create a directory with all the necessary files, which can then be transferred to another MAC...

```bash
[~/Projects/HelloWorld/HelloWorld] dotnet publish -r osx-x64
Microsoft (R) Build Engine version 16.2.37902+b5aaefc9f for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 9.29 sec for /Users/compsci/Projects/HelloWorld/HelloWorld/HelloWorld.csproj.
  HelloWorld -> /Users/compsci/Projects/HelloWorld/HelloWorld/bin/Debug/netcoreapp2.1/osx-x64/HelloWorld.dll
  HelloWorld -> /Users/compsci/Projects/HelloWorld/HelloWorld/bin/Debug/netcoreapp2.1/osx-x64/publish/
[~/Projects/HelloWorld/HelloWorld] dir
total 16
drwxr-xr-x   6 compsci  staff  192  2 Sep 15:41 .
drwxr-xr-x   6 compsci  staff  192  8 Sep 14:51 ..
-rw-r--r--   1 compsci  staff  178  2 Sep 15:41 HelloWorld.csproj
-rw-r--r--   1 compsci  staff  192  2 Sep 15:41 Program.cs
drwxr-xr-x   3 compsci  staff   96  2 Sep 15:41 bin
drwxr-xr-x  10 compsci  staff  320  8 Sep 15:02 obj
[~/Projects/HelloWorld/HelloWorld] cd bin/Debug/netcoreapp2.1/osx-x64/publish/

```

## Running the 'published' code
```bash
[~/Projects/HelloWorld/HelloWorld/bin/Debug/netcoreapp2.1/osx-x64/publish] ./HelloWorld 
Hello World!

```

