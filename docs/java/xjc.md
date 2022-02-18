

## xjc aka generate POJO classes from XSD

**Note 1**: the `xjc` tool is only available until version JDK 1.8


```
.\xjc.exe -nv -d C:\Users\m.giordano\IdeaProjects\ReCargo\Data\src\main\java\ -p it.sisnet.recargo.xsd.costa C:\Users\m.giordano\Desktop\temp\G4.xsd
```

Where the *-d* parameter sets the output directory where the java files will be created and the *-p* parametere will set the name of the package.



