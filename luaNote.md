# 编译lua源码
生成built_lua.bat
```
set path=I:\InstallerPackage\VisualStudio\vs2010_Compiler-2018-09-07-17-14\Compiler\VC\bin;%path%

call vcvars32.bat

set path=I:\InstallerPackage\VisualStudio\vs2010_Compiler-2018-09-07-17-14\Compiler\VC\include;%path%

mkdir bin
cd src
del *.obj
cl /O2 /W3 /c /DLUA_BUILD_AS_DLL *.c
del lua.obj luac.obj
link /Dll /out:../bin/lua.dll *.obj

cl /O2 /W3 /c /DLUA_BUILD_AS_DLL lua.c luac.c
link /Dll /out:../bin/lua.exe lua.obj ../bin/lua.lib
del lua.obj

link /out:../bin/luac.exe *.obj
del *.obj
cd ..
```

编译过程中，可能遇到以下问题
```
loadlib.c(180) : fatal error C1083: 无法打开包括文件:“windows.h”: No such file or directory
```

遇到这个报错，说明 VS命令行找不到 windows SDK，就要手动改下 VS命令行脚本。

# Microsoft SDKS

微软软件开发工具包（SDK），它提供文档的链接，代码示例，工具，标题，库，和其他文件，开发人员可以使用它来创建软件应用程序和库。