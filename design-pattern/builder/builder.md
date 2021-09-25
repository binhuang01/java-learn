# Builder(建造者模式)

## 1.定义

​		将一个复杂对象的构造与它的表示分离，使用同样的构建过程可以创建不同的对象。它将一个复杂对象分解为多个简单对象，然后一步步构建而成。



## 2.特点

​		1.封装性好，构建与表示分离。

​		2.扩展性好，各个具体建造者互相独立，有利于系统解耦。

​		3.使用者不需知道对象创建细节，不对其他模块产生影响。

​		缺点：

   	 1.产品的组成部分必须相同，限制了使用范围。

​		2.如果产品内部变化复杂，当内部发生变化时，建造者也要同步更改，后期维护成本比较大。



## 3.使用场景

​		1.当一个类的构造函数参数超过4个，而且这些参数有些是可选的参数，考虑使用构造者模式。

​		2.相同的方法，不同执行顺序，产生不同的结果



## 4.结构与实现

​	1. Object (要构造的对象)

​	2. AbstractBuilder (抽象建造者)

​	3. ConcreteBuilder (具体建造者)

​	4. Director (统一组建过程)

![image-20210925194112331](C:\Users\asus\Desktop\dairy\image-20210925194112331.png)

​										uml结构图

实现：

1. 产品类

```java
class Product {
    private String partA;
    private String partB;
    private String partC;
    public void setPartA(String partA) {
        this.partA = partA;
    }
    public void setPartB(String partB) {
        this.partB = partB;
    }
    public void setPartC(String partC) {
        this.partC = partC;
    }
    public void show() {
        //显示产品的特性
    }
}
```



2.抽象建造者

```java
abstract class Builder {
    //创建产品对象
    protected Product product = new Product();
    public abstract void buildPartA();
    public abstract void buildPartB();
    public abstract void buildPartC();
    //返回产品对象
    public Product getResult() {
        return product;
    }
}
```



3.具体建造者

```java
public class ConcreteBuilder extends Builder {
    public void buildPartA() {
        product.setPartA("建造 PartA");
    }
    public void buildPartB() {
        product.setPartB("建造 PartB");
    }
    public void buildPartC() {
        product.setPartC("建造 PartC");
    }
}
```



4.指挥者

```java
class Director {
    private Builder builder;
    public Director(Builder builder) {
        this.builder = builder;
    }
    //产品构建与组装方法
    public Product construct() {
        builder.buildPartA();
        builder.buildPartB();
        builder.buildPartC();
        return builder.getResult();
    }
}
```



5.使用者

```java
public class Client {
    public static void main(String[] args) {
        Builder builder = new ConcreteBuilder();
        Director director = new Director(builder);
        Product product = director.construct();
        product.show();
    }
}
```





## 5.与工厂模式的区别

- 建造者模式更加注重方法的调用顺序，工厂模式注重创建对象。
- 创建对象的力度不同，建造者模式创建复杂的对象，由各种复杂的部件组成，工厂模式创建出来的对象都一样
- 关注重点不一样，工厂模式只需要把对象创建出来就可以了，而建造者模式不仅要创建出对象，还要知道对象由哪些部件组成。
- 建造者模式根据建造过程中的顺序不一样，最终对象部件组成也不一样。







## 6.参考

------[秒懂设计模式之建造者模式（Builder pattern）_ShuSheng007的程序人生-CSDN博客](https://blog.csdn.net/ShuSheng0007/article/details/86619675)