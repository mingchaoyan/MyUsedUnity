# JSON 序列化

JSON序列化功能可以使Unity对象和JSON格式之间互相转化。这在和Web服务器交互，或者打包解包文本格式的数据的情况下非常方便。

## 简单例子

JSON序列化功能围绕“结构化”JSON这个概念，所以你在class或者structure中描述的数据将会被存到JSON数据。如：
```cs

```
定义了一个普通的C#类，它包含三个变量level,timeElapsed, playerName，标记它为 Serializable(JSON 序列器必须)。你可以如下创建实例：
```cs
```

使用JsonUtility.ToJson可以序列化成JSON
```cs
string json = JsonUtility.ToJson(myObject);
```
如此创建一个包含了字符串的json变量
``cs
{"level":1,"timeElapsed":47.5, "playerName":"Dr Charles Francis"}
``
把这个JSON转回成对象，使用JsonUtility.FromJson:
```cs
myObject = JsonUtility.FromJson<MyClass>(json);
```
如果JSON数据中包含MyClass中没有的字段，数据将被忽略，如果JSON数据中没有MyClass中的字段，那按照MyClass构造函数中构造的初始值给这个字段赋值。

目前不支持非格式化的JSON，如果你需要这样的功能，需要去寻找功能更丰富的JSON库。

## 用JSON覆盖对象

可以使用JSON数据去覆盖一个已经存在的对象。
```CS
JsonUtility.FromJsonOverwrite(json, myObject);
```
JSON数据没有的字段将不产生改变。该方法将允许你可以分配最小的资源重用一个已经创建的对象。同时也可以用JSON给一个对象打补丁

注意，JSON 序列器的API提供了Monobehavior和ScriptableObject的子类，当反序列化Monobehavior和ScriptableObject的子类时，需要使用FromJsonOverwrite；FromJson将会抛出异常

## 支持的类型

Monobehaviour的子类，ScriptableObject的子类和其他使用[Serializable]属性的类。对象传给标准Unity序列器，所以规则和限制是一样的，只有字段会被序列化，另外一些诸如Dictionary<>这些负责的不支持

其他类型(比如原始类型或者数组)直接传给API，也是不支持的，你需要把它们包在一个类或者结构中

编辑器代码也有相对的API-EditorJsonUtility，它将允许你序列化／反序列化所有从UnityEngine.Object中派生的类。这将产生和YAML表现一样的数据

## 性能

Benchmark 显示类JsonUtility比.NET JSON 方法会快很多（尽管功能也少了很多）

GC 内存的使用也是尽可能少
* ToJson() 只给返回的字符串分配 GC 内存
* FromJson() 只给返回的对象(包括子对象) 分配内存
* FromJsonOverwrite() 只给需要写入的字段分配内存，如果所有字段都已经赋值，将不产生GC内存

在后台线程使用JsonUtility API 是 **禁止**的。因为多线程的代码你将需要非常小心的处理正在被另一个线程修改的对象

## 预先不知道类型的情况下使用FromJson() TODO

反序列化一个JSON为包含普通字段的类和结构，然后使用
