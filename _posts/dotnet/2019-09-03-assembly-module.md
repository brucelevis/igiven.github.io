





# 关于模块

单文件程序集是一个独立、单一且定义明确的包，这个包中包含所有必需的CIL、元数据和相关的程序集清单。

另一方面，多文件程序集则由多个.NET二进制文件组成，其中的每个二进制文件称作模块（module）。生成一个多文件程序集时，其中一个模块（称为主模块）一定包含程序集清单（还可能包含CIL指令和各种类型元数据）。其他相关的模块包含一个模块级的程序集清单、CIL和类型元数据。可以想到，主模块会记录程序集清单中所含的其他必要的辅助模块



https://docs.microsoft.com/zh-cn/dotnet/framework/app-domains/how-to-build-a-multifile-assembly

