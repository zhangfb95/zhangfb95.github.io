---
layout: post
title:  观察者模式
date:   2018-10-26 23:33:00 +0800
categories: 设计模式
tag: 设计模式
---

* content
{:toc}

### 简介

观察者模式用于将两个耦合的对象以事件的方式进行分离，从而降低其耦合度。

### 示例

```java
public class Observable {
    
    private List<Observer> observers;
    
    public Observable() {
        observers = new ArrayList<>();
    }
    
    public void add(Observer observer) {
        this.observers.add(observer);
    }
    
    public void notify() {
        this.notify(null);
    }
    
    public void notify(Object msg) {
        for (Observer observer : observers) {
            observer.update(this, msg);
        }
    }
} 

public interface Observer {

    void update(Observable o, Object msg);
}

public class Main {

    public static void main(String[] args) {
        Observable observable = new Observable();
        observable.add(new AObserver());
        observable.add(new BObserver());
        observable.notify("hello observer!");
    }
}
```