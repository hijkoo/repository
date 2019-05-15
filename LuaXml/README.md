# LuaXml


## 功能说明

LUA在字符串处理上虽然比较方便，但是直接是同string操作XML还是比较麻烦的。LuaXML就是专为了处理XML而编写的第三方库，LuaXML不光能用于lua脚本同事也提供了C语言的支持

## 核心文件介绍

1. LuaXml.lua lua引入文件
2. LuaXML_lib.so so库文件
3. Makefile 编译以上两个文件的makefile,若重新编译见,https://github.com/LuaDist/luaxml .

## 使用流程

1. 下载 luaxml 安装文件，替换或修改Makefile文件 。
2. 执行make clean &&  make 操作
3. 将LuaXml.lua LuaXml_lib.so 复制到你到lualib库（如：/home/pubsrv/openresty/lualib）
