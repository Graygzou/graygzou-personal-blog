---
Title: .NET and Common Language Runtime (CLR)
Description: TODO
Date: TODO
tags: ["c#", "java"]
draft: true
---

# Java JVM vs C# CLR
digraph G {
aize ="4,4";
    main [shape=box];
    main -> parse [weight=8];
    parse -> execute;
    main -> init [style=dotted];
    main -> cleanup;
    execute -> { make_string; printf}
    init -> make_string;
    edge [color=red];
    main -> printf [style=bold,label="100 times"];
    make_string [label="make a string"];
    node [shape=box,style=filled,color=".7 .3 1.0"];
    execute -> compare;
  }
)

## Acknowledgment
* [Stackoverflow - Java's Virtual Machine and CLR](https://stackoverflow.com/questions/453610/javas-virtual-machine-and-clr)
* [Stackoverflow - compilation process : Java Runtime Environment compare .NET framework](https://stackoverflow.com/questions/11253303/how-does-the-java-runtime-environment-compare-with-the-net-framework-in-terms-o)
* [Microsoft docs - Common Language Runtime (CLR) overview](https://docs.microsoft.com/en-us/dotnet/standard/clr)
* [Stackoverflow - Differences between MSIL and Java bytecode](https://stackoverflow.com/questions/95163/differences-between-msil-and-java-bytecode)
* [google image](https://www.google.com/search?biw=1598&bih=797&tbm=isch&sa=1&ei=JRpuXPC1KsGZ_QbE85jYBg&q=java+compilation+vs+clr+compilation&oq=java+compilation+vs+clr+compilation&gs_l=img.3...12465.17023..17189...0.0..2.338.2392.13j2j2j2......0....1..gws-wiz-img.......0j0i30j0i8i30j0i24.YU0HGeg8iJU#imgrc=R3EUOmJzAZcxrM:)
