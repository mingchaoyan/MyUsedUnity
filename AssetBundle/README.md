# AssetBundle

## 0. 前言-Unity中的资源

### 0.0 自动打包资源（静态）
* 场景中直接使用的资源会随着场景被自动打包进游戏，同时在场景加载时也会自动加载这些资源。这些资源只要放在Assets/目录下即可；
* 一般Demo类的小游戏才使用此法。

### 0.1 Resources资源
* Assets/Resources 目录下的所有资源都会被打包进游戏，可以通过Resources.Load加载；
* 开发时为了方便（不用在更改资源后重新打包）一般都使用此法。

### 0.2 AssetBundle资源
* 通过编辑器脚本将资源打包成多个独立的AssetBundle，可以通过WWW类加载；
* 发布时考虑到把一开始玩家玩不到的内容做成增量包减少包体积，以及热更新修复Bug，一般使用此法。

## 1. 官方手册

### 1.0 导言

#### 1.0.0 开发时

0. 打包好AB
1. 上传AB到服务器

#### 1.0.1 玩家玩游戏时

0. 从服务器下载AB
1. 从AB中加载需要的资源

### 1.1 打包AB

#### 1.1.0 使用BuildPipeline.BuildAssetBundle导出
0. 在Inspector底部标记本资源需要打包进的AB
1. BuildPipeline.BuildAssetBundle打包已经被标记的资源

#### 1.1.1 使用AssetDatabase.GetAllAssetBundleNames获取AB名字
```cs
using UnityEditor;
using UnityEngine;

public class GetAssetBundleNames
{
    [MenuItem ("Assets/Get AssetBundle names")]
    static void GetNames ()
    {
        var names = AssetDatabase.GetAllAssetBundleNames();
        foreach (var name in names)
        Debug.Log ("AssetBundle: " + name);
    }
}
```

#### 1.1.2 使用OnPostprocessAssetbundleNameChanged告知开发者,资源改变了AB
```CS
using UnityEngine;
using UnityEditor;

public class MyPostprocessor : AssetPostprocessor {
    void OnPostprocessAssetbundleNameChanged ( string path, string previous, string next)
    { 
        Debug.Log("AB: " + path + " old: " + previous + " new: " + next); 
    } 
}
```

#### 1.1.3 AssetBundle 变量

### 1.2 一堆API

