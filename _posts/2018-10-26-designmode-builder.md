---
layout: post
title:  构建者模式
date:   2018-10-26 23:31:00 +0800
categories: 设计模式
tag: 设计模式
---

* content
{:toc}

### 简介

创建者模式将一个复杂对象的创建和其表示进行分离，创建者模式将创建的过程抽象化，使其创建可以使用增加子类的方式动态进行扩展。

### 示例1

一个具体的产品

```java
public class Product {

    private List<String> parts = new ArrayList<>();

    public void add(String part) {
        this.parts.add(part);
    }

    @Override public String toString() {
        return "parts: " + parts;
    }
}
```

构建者的抽象

```java
public interface Builder {

    Builder instance();
    Builder buildPartA();
    Builder buildPartB();
    Builder buildPartC();
    Product build();
}
```

构建者的实现

```java
public class BuilderA implements Builder {

    private Product product;

    @Override public Builder instance() {
        product = new Product();
        return this;
    }

    @Override public Builder buildPartA() {
        product.add("build a: part a");
        return this;
    }

    @Override public Builder buildPartB() {
        product.add("build a: part b");
        return this;
    }

    @Override public Builder buildPartC() {
        product.add("build a: part c");
        return this;
    }

    @Override public Product build() {
        return this.product;
    }
}
```

导演类

```java
public class Director {

    private Builder builder;

    public Director(Builder builder) {
        this.builder = builder;
    }

    public Product build() {
        return builder.instance().buildPartA().buildPartB().buildPartC().build();
    }
}
```

调用客户端

```java
public class Main {

    public static void main(String[] args) {
        Builder builder = new BuilderA();
        Director director = new Director(builder);
        Product product = director.build();
        System.out.println(product);
    }
}
```

### 示例2，lombok的@Builder实现

```java
@Builder @Data public class Product {

    private List<String> parts = new ArrayList<>();
}
```

```java
public class Main {

    public static void main(String[] args) {
        Product product = Product.builder().parts(Arrays.asList("a", "b", "c")).build();
        System.out.println(product);
    }
}
```