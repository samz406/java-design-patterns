---
layout: pattern
设计模式名: 建造者模式
文件名: builder
permalink: /patterns/builder/
类型: 创建型模式
tags:
 - Java
 - Gang Of Four
 - Difficulty-Intermediate
---

## 目的
将复杂对象的构建与它的表示分离，使得同样的构建可以创建不同的表示

## 举例说明

真实的例子

>想象一下角色扮演游戏的角色生成器， 最简单的选择是让电脑为你创造角色。 但是，如果你想选择职业，性别，头发颜色等字符细节角色生成会一步一步的构造，直到角色全部构造完成

简单的描述

> 允许您创建不同风格的对象，同时避免构造器污染。 当可能有几种风格的对象时很有用。 或者当创建对象时涉及很多步骤。

Wikipedia says

> 构建器模式是一种对象创建软件设计模式，旨在寻找伸缩构造器反模式的解决方案

话虽如此，让我补充一点关于伸缩构造函数反模式的内容。 在某一点或其他我们都看到了像下面这样的构造函数:

```
public Hero(Profession profession, String name, HairType hairType, HairColor hairColor, Armor armor, Weapon weapon) {
}
```

正如您所看到的，构造函数参数的数量可能会很快失去控制，并且可能很难理解参数的排列方式。 此外，如果您希望在未来添加更多选项，此参数列表可能会持续增长。 这被称为伸缩式构造函数反模式。

**代码示例**

理智的选择是使用构造者模式， 首先，我们有我们想要创造的英雄

```
public final class Hero {
  private final Profession profession;
  private final String name;
  private final HairType hairType;
  private final HairColor hairColor;
  private final Armor armor;
  private final Weapon weapon;

  private Hero(Builder builder) {
    this.profession = builder.profession;
    this.name = builder.name;
    this.hairColor = builder.hairColor;
    this.hairType = builder.hairType;
    this.weapon = builder.weapon;
    this.armor = builder.armor;
  }
}
```

然后再创建一个builder

```
  public static class Builder {
    private final Profession profession;
    private final String name;
    private HairType hairType;
    private HairColor hairColor;
    private Armor armor;
    private Weapon weapon;

    public Builder(Profession profession, String name) {
      if (profession == null || name == null) {
        throw new IllegalArgumentException("profession and name can not be null");
      }
      this.profession = profession;
      this.name = name;
    }

    public Builder withHairType(HairType hairType) {
      this.hairType = hairType;
      return this;
    }

    public Builder withHairColor(HairColor hairColor) {
      this.hairColor = hairColor;
      return this;
    }

    public Builder withArmor(Armor armor) {
      this.armor = armor;
      return this;
    }

    public Builder withWeapon(Weapon weapon) {
      this.weapon = weapon;
      return this;
    }

    public Hero build() {
      return new Hero(this);
    }
  }
```

按照下面方式调用:

```
Hero mage = new Hero.Builder(Profession.MAGE, "Riobard").withHairColor(HairColor.BLACK).withWeapon(Weapon.DAGGER).build();
```

## 使用范围
在使用创建者模式时

* 用于创建复杂对象的算法应该独立于构成对象的部件以及它们的组装方式
* 构造过程必须允许对构建的对象进行不同的表示

## 实际使用的例子

* [java.lang.StringBuilder](http://docs.oracle.com/javase/8/docs/api/java/lang/StringBuilder.html)
* [java.nio.ByteBuffer](http://docs.oracle.com/javase/8/docs/api/java/nio/ByteBuffer.html#put-byte-) as well as similar buffers such as FloatBuffer, IntBuffer and so on.
* [java.lang.StringBuffer](http://docs.oracle.com/javase/8/docs/api/java/lang/StringBuffer.html#append-boolean-)
* All implementations of [java.lang.Appendable](http://docs.oracle.com/javase/8/docs/api/java/lang/Appendable.html)
* [Apache Camel builders](https://github.com/apache/camel/tree/0e195428ee04531be27a0b659005e3aa8d159d23/camel-core/src/main/java/org/apache/camel/builder)

## 参考资料

* [Design Patterns: Elements of Reusable Object-Oriented Software](http://www.amazon.com/Design-Patterns-Elements-Reusable-Object-Oriented/dp/0201633612)
* [Effective Java (2nd Edition)](http://www.amazon.com/Effective-Java-Edition-Joshua-Bloch/dp/0321356683)
