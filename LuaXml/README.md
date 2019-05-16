# LuaXml


## 功能说明

LuaXML就是专为了处理XML而编写的第三方库，LuaXML不光能用于lua脚本同时也提供了C语言的支持 。

## 核心文件介绍

1. LuaXml.lua lua引入文件 。
2. LuaXML_lib.so so库文件 。
3. Makefile 编译以上两个文件的makefile,若重新编译见,https://github.com/LuaDist/luaxml 。

## 编译流程

1. 下载 luaxml 安装文件，替换或修改Makefile文件 。
2. 执行make clean &&  make 操作 。
3. 将LuaXml.lua LuaXml_lib.so 复制到你到lualib库（如：/home/pubsrv/openresty/lualib）。

## 使用介绍

1. 常用函数： 
xml.new(arg)
创建一个新的XML对象
xml.append(var,tag)
添加一个子节点
xml.load(filename)
加载XML文件
xml.save(var,filename)
保存XML文件
xml.eval(xmlstring)
解析XML字符串
xml.tag(var, tag)
设置或返回一个XML对象
xml.str(var, indent, tag)
以字符串形式返回XML
xml.find(var, tag, attributeKey,attributeValue)
查找子节点
xml.registerCode(decoded,encoded)

2. 代码案例：

XML文件
```
<test>
	<item id="1">
		<field name="aa" />
		<field name="bb" />
	</item>
</test>
```

```
-- 导入依赖文件
require('LuaXml')

-- 加载XML文件
local xfile = xml.load("test.xml")
-- 查找子节点
local item = xfile:find("item")
-- 节点不为空
if item ~= nil then
 -- 节点对应键值
 print( item.id);

 -- 修改键值
 item.id = "abc";
 print( item.id);

 -- 第一个子节点
 local field = item[1];
 print( field);
 print( field.name);
 
 -- 获得子节点数量
 print( table.getn( item));

end

-- 添加子节点
local xNewFile = xml.new("root");
-- 设置子节点键值
local child = xNewFile:append("child");
child.id = 1;
xNewFile:append("child").id = 2;

-- 添加text节点
xNewFile:append("text")[1] = 'test';

print( xNewFile);
-- 保存文件
xNewFile:save"t.xml";
```
