---
layout: post
title:  模板模式
date:   2018-10-26 23:27:00 +0800
categories: 设计模式
tag: 设计模式
---

* content
{:toc}

### 概念

模式，通俗地讲就是固定的模式。类似地，模板就是固定的刻板。它刻画出轮廓，而轮廓通常就是`不变`的抽象。
模板模式，就是讲不变的内容抽象到父类，而变化的内容延迟到子类，不同的子类可以有不同的变化。
换句话说，我们的逻辑可分为两类，一类为通用，另一类为专用。而模板模式就是以父子类的方式解耦通用和专用。

### 示例

```java
public class Main {

    public static void main(String[] args) {
        Daily daily = new ZhangsanDaily();
        daily.doSomething();
        daily = new LisiDaily();
        daily.doSomething();
    }

    public static abstract class Daily {

        public void doSomething() {
            wakeup();
            eat();
            work();
            goToBed();
        }

        protected abstract void wakeup();

        protected abstract void eat();

        protected abstract void work();

        protected abstract void goToBed();
    }

    public static class ZhangsanDaily extends Daily {

        @Override protected void wakeup() {
            System.out.println("zhangsan's wakeup");
        }

        @Override protected void eat() {
            System.out.println("zhangsan's eat");
        }

        @Override protected void work() {
            System.out.println("zhangsan's work");
        }

        @Override protected void goToBed() {
            System.out.println("zhangsan's go to bed");
        }
    }

    public static class LisiDaily extends Daily {

        @Override protected void wakeup() {
            System.out.println("lisi's wakeup");
        }

        @Override protected void eat() {
            System.out.println("lisi's eat");
        }

        @Override protected void work() {
            System.out.println("lisi's work");
        }

        @Override protected void goToBed() {
            System.out.println("lisi's go to bed");
        }
    }
}
```