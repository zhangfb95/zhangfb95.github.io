---
layout: post
title:  策略模式
date:   2018-10-26 23:28:00 +0800
categories: 设计模式
tag: 设计模式
---

* content
{:toc}

### 概念

只有在存在多种方式的情况下，才有策略的概念。所以策略模式要解决的问题就是，根据不同的条件来达到不同目的。
最最大众化的策略模式莫过于条件分支，不同的if会有不同的代码块，这或许在很多人眼里不认为是策略模式。

随之而来的则有两种演变的变种

1. 基于面向对象的思想，我们将if代码块抽象成一个个的策略对象，那么就变成了面向对象的策略模式；
2. 我们将条件抽离到策略对象中，并简化成一个个枚举常量，这进一步增加了策略模式的灵活性。

### 示例1，最简单的面向对象策略模式

```java
public class Main {

    public static void main(String[] args) {
        System.out.println(calc("+", 9, 6));
    }

    private static int calc(String op, int a, int b) {
        if ("+".equals(op)) {
            return new Add().calc(a, b);
        } else if ("-".equals(op)) {
            return new Sub().calc(a, b);
        } else if ("*".equals(op)) {
            return new Multi().calc(a, b);
        }
        throw new UnsupportedOperationException("不支持的操作方式");
    }

    public static class Add {

        int calc(int a, int b) {
            return a + b;
        }
    }

    public static class Sub {

        int calc(int a, int b) {
            return a - b;
        }
    }

    public static class Multi {

        int calc(int a, int b) {
            return a * b;
        }
    }
}
```

### 示例2，进一步抽象

```java
public class Main {

    public static void main(String[] args) {
        System.out.println(calc("+", 9, 6));
    }

    private static final Map<OpEnum, Op> opMap = new HashMap<OpEnum, Op>() {
        {
            List<Op> ops = Arrays.asList(new Add(), new Sub(), new Multi());
            for (Op op : ops) {
                put(op.supported(), op);
            }
        }
    };

    private static int calc(String op, int a, int b) {
        for (OpEnum opEnum : OpEnum.values()) {
            if (opEnum.code.equals(op)) {
                return opMap.get(opEnum).calc(a, b);
            }
        }
        throw new UnsupportedOperationException("不支持的操作方式");
    }

    interface Op {

        OpEnum supported();

        int calc(int a, int b);
    }

    public static class Add implements Op {

        @Override public OpEnum supported() {
            return OpEnum.add;
        }

        @Override public int calc(int a, int b) {
            return a + b;
        }
    }

    public static class Sub implements Op {

        @Override public OpEnum supported() {
            return OpEnum.sub;
        }

        @Override public int calc(int a, int b) {
            return a - b;
        }
    }

    public static class Multi implements Op {

        @Override public OpEnum supported() {
            return OpEnum.multi;
        }

        @Override public int calc(int a, int b) {
            return a * b;
        }
    }

    public enum OpEnum {

        add("+"),
        sub("-"),
        multi("*");

        private String code;

        OpEnum(String code) {
            this.code = code;
        }
    }
}
```