

## xjc aka generate POJO classes from XSD

**Note 1**: the `xjc` tool is only available until version JDK 1.8


```
.\xjc.exe -nv -d C:\Users\m.giordano\IdeaProjects\FlussiCosta\src\main\java\ -p it.sisnet.seven.acquisizione.costa.xsd "c:\Users\m.giordano\Documents\progetti\2021.12 - Temporanea custodia - H2 custom Costa\XSD\dichiarazioneH2_AcquisizioneFlussi_v1.xsd" -encoding UTF-8
```

Where the *-d* parameter sets the output **base** directory where the java files will be created and the *-p* parameter will set the name of the package.


