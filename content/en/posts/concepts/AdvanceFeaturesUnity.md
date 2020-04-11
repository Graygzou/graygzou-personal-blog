---
Title: .NET and Common Language Runtime (CLR)
Description: TODO
Date: TODO
tags: ["c#"]
draft: true
---

# Advance Features

## Managed plugins
|             | .NET Standard 2.0 | .NET 4.x |
| ----------- | :----: | :----: |
| .NET Standard      | Supported       | Supported       |
| .NET Framework   | Limited        | Supported        |
| .NET Core   | Not Supported        | Not Supported        |

**Note:**
* Managed plugins compiled against any version of the .NET Standard work with Unity.
* Limited support indicates that Unity supports the configuration if all APIs used from the .NET Framework are present in the .NET Standard 2.0 profile. However, the .NET Framework API is a superset of the .NET Standard 2.0 profile, so some APIs are not available.

## References
* [Unity Manual - .NET profile support](https://docs.unity3d.com/Manual//dotnetProfileSupport.html)
