# PublishError
Repository to reproduce a dotnet publish error

# [Submitted Issue](https://github.com/dotnet/sdk/issues/28403)
### Describe the bug
When trying to publish a WPF application with `dotnet publish -p:PublishProfile=ClickOnceProfile` I get `error MSB4062: The "Microsoft.Build.Tasks.RequiresFramework35SP1Assembly" task could not be loaded...`. Publishing in Visual Studio works fine.

The computer I wrote this on did have SDK 7.0.100-rc.1.22431.12 installed but others running SDK 6.0.401 also had this issue.

### To Reproduce (Using Visual Studio 2022)
1. Create new WPF project (net6.0)
    a. Repo of the project I pulled [https://github.com/ecassidy-etc/PublishError](https://github.com/ecassidy-etc/PublishError)
3. Create publish ClickOnce profile (next through wizard to take defaults)
4. Open a terminal to the project root
5. Run `dotnet build` to verify it builds
6. Run `dotnet publish -p:PublishProfile=ClickOnceProfile`

### Output
```
MSBuild version 17.4.0-preview-22428-01+14c24b2d3 for .NET
  Determining projects to restore...
  All projects are up-to-date for restore.
C:\Program Files\dotnet\sdk\7.0.100-rc.1.22431.12\Sdks\Microsoft.NET.Sdk\targets\Microsoft.NET.RuntimeIdentifierInferen
ce.targets(219,5): message NETSDK1057: You are using a preview version of .NET. See: https://aka.ms/dotnet-support-poli
cy [C:\Users\eric.cassidy\source\repos\PublishError\PublishError.csproj]
C:\Program Files\dotnet\sdk\7.0.100-rc.1.22431.12\Microsoft.Common.CurrentVersion.targets(4147,5): error MSB4062: The "
Microsoft.Build.Tasks.RequiresFramework35SP1Assembly" task could not be loaded from the assembly Microsoft.Build.Tasks.
Core, Version=15.1.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a.  Confirm that the <UsingTask> declaration is
correct, that the assembly and all its dependencies are available, and that the task contains a public class that imple
ments Microsoft.Build.Framework.ITask. [C:\Users\eric.cassidy\source\repos\PublishError\PublishError.csproj]
```

### Exception
```
C:\Program Files\dotnet\sdk\7.0.100-rc.1.22431.12\Microsoft.Common.CurrentVersion.targets(4147,5): error MSB4062: The "
Microsoft.Build.Tasks.RequiresFramework35SP1Assembly" task could not be loaded from the assembly Microsoft.Build.Tasks.
Core, Version=15.1.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a.  Confirm that the <UsingTask> declaration is
correct, that the assembly and all its dependencies are available, and that the task contains a public class that imple
ments Microsoft.Build.Framework.ITask. [C:\Users\eric.cassidy\source\repos\PublishError\PublishError.csproj]
```

### Further technical details
- Include the output of `dotnet --info`
```
.NET SDK:
 Version:   7.0.100-rc.1.22431.12
 Commit:    f1cf61e1c0

Runtime Environment:
 OS Name:     Windows
 OS Version:  10.0.19044
 OS Platform: Windows
 RID:         win10-x64
 Base Path:   C:\Program Files\dotnet\sdk\7.0.100-rc.1.22431.12\

Host:
  Version:      7.0.0-rc.1.22426.10
  Architecture: x64
  Commit:       06aceb7015

.NET SDKs installed:
  2.1.202 [C:\Program Files\dotnet\sdk]
  7.0.101 [C:\Program Files\dotnet\sdk]
  6.0.401 [C:\Program Files\dotnet\sdk]
  8.0.100-rc.1.22431.12 [C:\Program Files\dotnet\sdk]

.NET runtimes installed:
  Microsoft.AspNetCore.App 6.0.1 [C:\Program Files\dotnet\shared\Microsoft.AspNetCore.App]
  Microsoft.AspNetCore.App 6.0.9 [C:\Program Files\dotnet\shared\Microsoft.AspNetCore.App]
  Microsoft.AspNetCore.App 7.0.0-rc.1.22427.2 [C:\Program Files\dotnet\shared\Microsoft.AspNetCore.App]
  Microsoft.NETCore.App 2.0.9 [C:\Program Files\dotnet\shared\Microsoft.NETCore.App]
  Microsoft.NETCore.App 3.1.23 [C:\Program Files\dotnet\shared\Microsoft.NETCore.App]
  Microsoft.NETCore.App 5.0.14 [C:\Program Files\dotnet\shared\Microsoft.NETCore.App]
  Microsoft.NETCore.App 6.0.1 [C:\Program Files\dotnet\shared\Microsoft.NETCore.App]
  Microsoft.NETCore.App 6.0.7 [C:\Program Files\dotnet\shared\Microsoft.NETCore.App]
  Microsoft.NETCore.App 6.0.9 [C:\Program Files\dotnet\shared\Microsoft.NETCore.App]
  Microsoft.NETCore.App 7.0.0-rc.1.22426.10 [C:\Program Files\dotnet\shared\Microsoft.NETCore.App]
  Microsoft.WindowsDesktop.App 3.1.14 [C:\Program Files\dotnet\shared\Microsoft.WindowsDesktop.App]
  Microsoft.WindowsDesktop.App 3.1.23 [C:\Program Files\dotnet\shared\Microsoft.WindowsDesktop.App]
  Microsoft.WindowsDesktop.App 5.0.14 [C:\Program Files\dotnet\shared\Microsoft.WindowsDesktop.App]
  Microsoft.WindowsDesktop.App 6.0.1 [C:\Program Files\dotnet\shared\Microsoft.WindowsDesktop.App]
  Microsoft.WindowsDesktop.App 6.0.2 [C:\Program Files\dotnet\shared\Microsoft.WindowsDesktop.App]
  Microsoft.WindowsDesktop.App 6.0.7 [C:\Program Files\dotnet\shared\Microsoft.WindowsDesktop.App]
  Microsoft.WindowsDesktop.App 6.0.9 [C:\Program Files\dotnet\shared\Microsoft.WindowsDesktop.App]
  Microsoft.WindowsDesktop.App 7.0.0-rc.1.22427.1 [C:\Program Files\dotnet\shared\Microsoft.WindowsDesktop.App]

Other architectures found:
  x86   [C:\Program Files (x86)\dotnet]

Environment variables:
  Not set

global.json file:
  Not found

Learn more:
  https://aka.ms/dotnet/info

Download .NET:
  https://aka.ms/dotnet/download
```
- The IDE (VS / VS Code/ VS4Mac) you're running on, and its version
```
Microsoft Visual Studio Professional 2022
Version 17.3.5
VisualStudio.17.Release/17.3.5+32922.545
Microsoft .NET Framework
Version 4.8.04084

Installed Version: Professional

ASP.NET and Web Tools   17.3.376.3011
ASP.NET and Web Tools

Azure App Service Tools v3.0.0   17.3.376.3011
Azure App Service Tools v3.0.0

C# Tools   4.3.0-3.22470.13+80a8ce8d5fdb9ceda4101e2acb8e8eb7be4ebcea
C# components used in the IDE. Depending on your project type and settings, a different version of the compiler may be used.

Common Azure Tools   1.10
Provides common services for use by Azure Mobile Services and Microsoft Azure Tools.

Microsoft JVM Debugger   1.0
Provides support for connecting the Visual Studio debugger to JDWP compatible Java Virtual Machines

NuGet Package Manager   6.3.0
NuGet Package Manager in Visual Studio. For more information about NuGet, visit https://docs.nuget.org/

TypeScript Tools   17.0.10701.2001
TypeScript Tools for Microsoft Visual Studio

Visual Basic Tools   4.3.0-3.22470.13+80a8ce8d5fdb9ceda4101e2acb8e8eb7be4ebcea
Visual Basic components used in the IDE. Depending on your project type and settings, a different version of the compiler may be used.

Visual F# Tools   17.1.0-beta.22363.4+1b94f89d4d1f41f20f9be73c76f4b229d4e49078
Microsoft Visual F# Tools

Visual Studio IntelliCode   2.2
AI-assisted development for Visual Studio.
```