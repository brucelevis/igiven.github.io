---
title:  "使用配置文件来管理NuGet包版本F"	
---









一个项目会引用很多的包,升级起来会很头疼,先上个连接





先创建一个文件`Directory.Build.props`

```
<Project>
    <PropertyGroup>
        <NuGet-Kritner-SolarProjection>1.0.2</NuGet-Kritner-SolarProjection>
    </PropertyGroup>
</Project>
```

然后修改你的项目文件

```
<ItemGroup>
  <PackageReference Include="Kritner.SolarProjection" Version="$(NuGet-Kritner-SolarProjection)" />
</ItemGroup>
```





### 相关连接

- [包的版本号](https://docs.microsoft.com/zh-cn/nuget/consume-packages/package-references-in-project-files)
- [Directory.Build.props的说明](https://docs.microsoft.com/zh-cn/visualstudio/msbuild/customize-your-build?view=vs-2019)

