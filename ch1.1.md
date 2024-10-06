传统方法，是将对象的创建由各自的调用者负责。工厂模式的主要思想是，将创建的功能封装在一个地方集中处理


\section{简单工厂}
将对象的创建集中到一个地方， 这样，如果需要修改，只需要修改一个地方。

class PizzaFactory {
public static Pizza createPizza(){
return null;
}
}
\section{工厂方法}
没有工厂类，User只是先在自己的类中创建一个抽象的“方法”，再将对象的实例化推迟到子类的“方法”中实现



\section{抽象工厂}
是简单工厂和工厂方法的结合。
专门搞一个抽象的工厂，将对象的实例化推迟到工厂的子类中实现。
User调用时，选择使用哪一个具体的工厂

abstract class AbsPizzaFactory

class BjPizzaFactory implements AbsPizzaFactory{
public Pizza createPizza(){
return null;
}
}


User
AbsPizzaFactory factory = null;




123）抽象工厂模式和原型模式之间的区别？(答案)