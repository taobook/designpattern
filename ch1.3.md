# 抽象工厂

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
