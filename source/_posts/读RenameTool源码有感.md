title: 读RenameTool源码有感
author: ismatch
tags: []
categories: []
date: 2019-03-06 23:32:00
---
#### RenameTool
- C#项目重命名工具
- [项目地址](https://github.com/liamwang/rename-tool)
- 实际使用过程中对于中文编码的处理还有问题，看了编码检测代码，感觉没啥问题...

#### 代码截取
- 一个控制台里封装用户输入的类,很有意思
```
public class CmdReader
    {
        public static string ReadLine(string tipText, Func<string, bool> validate = null)
        {
            var input = string.Empty;
            while (string.IsNullOrWhiteSpace(input) || (validate != null && !validate(input)))
            {
                Console.WriteLine(tipText);
                input = Console.ReadLine();
            }
            return input;
        }
    }
```
- 配置文件的处理，最近见到了许多类似的写法，一个静态方法实例化自己
```
public class Configuration
    {
        public IEnumerable<string> IgnoreFolders { get; set; } = new HashSet<string>();
        public IEnumerable<string> IgnoreExtensions { get; set; } = new HashSet<string>();
        public IEnumerable<string> CopyFolders { get; set; } = new HashSet<string>();

        public static Configuration Build()
        {
            var builder = new ConfigurationBuilder()
                .SetBasePath(Directory.GetCurrentDirectory())
                .AddJsonFile("appsettings.json");

            var config = builder.Build();

            return new Configuration
            {
                IgnoreFolders = config[nameof(IgnoreFolders)].TrimSplit(','),
                IgnoreExtensions = config[nameof(IgnoreExtensions)].TrimSplit(','),
                CopyFolders = config[nameof(CopyFolders)].TrimSplit(',')
            };
        }
    }
```
- 在vs里文件右键属性可以设置是否复制到输出目录，特别是针对于某些配置文件，生成或者发布项目的时候就可以带上配置文件，直到今天才知道有这个东西，实在忏愧
```
// 实际就是在项目文件里这么写 
// PreserveNewest：如果较新则复制 Always：始终复制
<ItemGroup>
    <None Update="appsettings.json">
      <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
    </None>
    <None Update="StartRename.bat">
      <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
    </None>
  </ItemGroup>
```