---
layout: post
title:  享元模式
date:   2018-10-26 23:29:00 +0800
categories: 设计模式
tag: 设计模式
---

* content
{:toc}

### 概念

享元模式，故名思议就是共享数据的意思。
常用的场景就是缓存，当加载的对象使用很频繁，同时加载又很慢时，我们可以考虑使用此模式。

### 示例

```java
public static class Obj {

    private Map<String, Object> loadedCacheMap;

    public void init() {
        // init loadedCachedMap...
    }

    /**
     * 可以在这些方法中使用缓存对象
     */
    public void calc() {
        System.out.println(loadedCachedMap);
    }
}
```