# Singleton

The singleton scope is the default scope in Spring. singleton (Default) Scopes a single bean definition to a single object instance per Spring IoC container.

### 1. 饿汉声明（推荐，功能正确，不节省空间，性能好）

```java
public class Singleton {
	//why no multiple instances?
	//becuase initialized during class loading stage
	//class loading is thread-safe
	//when will class is loaded?
	private static final Singleton instance = new Singleton();
	
	private Singleton(){
	}

	public static Singleton getInstance() {
		return instance;
	}
}
```


### 2. 饿汉静态代码快（推荐，功能正确，不节省空间，性能好）
same as 1

### 3. 懒汉不带锁（不推荐，功能不正确，节省空间，性能好）
```java
public class Singleton {
	private static Singleton instance;
	
	private Singleton(){
	}
	//no synchronized - incorrect
	public static Singleton getInstance() {
		if(instance==null) {
			instance = new Singleton();
		}
		return instance;
	}
}
```

### 4. 懒汉同步方法（不推荐，功能正确，节省空间，性能不好）
```java
public class Singleton {
	private static Singleton instance;
	
	private Singleton(){
	}
	
	public static synchronized Singleton getInstance() {
		if(instance==null) {
			instance = new Singleton();
		}
		return instance;
	}
}
```

### 5. 懒汉同步代码块单重检查（不推荐，功能不正确，节省空间，性能不好）
```java
public class Singleton {
	private static Singleton instance;
	
	private Singleton(){
	}
	
	public static Singleton getInstance() {
		if(instance==null) {
			//multiple threads are waiting here, and will create an instance each -- incorrect
			synchronized(Singleton.class) {//incorrect
				instance = new Singleton();
			}
		}
		return instance;
	}
}
```


### 6. 懒汉同步代码块双重检查（推荐，功能正确，节省空间，性能可以）
```java
public class Singleton {
	private static volatile Singleton instance;
	
	private Singleton(){
	}
	
	public static Singleton getInstance() {
		if(instance==null) {//could still be broken in managed code?
			//multiple threads are waiting here
			synchronized(Singleton.class) {
				if(instance==null) {//double checked //could still be broken in managed code?
					instance = new Singleton();
				}
			}
		}
		return instance;
	}
}
```


### 7. 静态内部类 （推荐）
利用了静态内部类默认不加载的特性，可以起到懒加载的好处--节省空间
利用了类加载时候的线程安全，满足了线程安全的需求
```java
public class Singleton {
	private static volatile Singleton instance;
	
	private Singleton(){
	}
	
	//is not loaded by default. only loaded when used.
	private static class SingletonInnerClass {
		private static final Singleton instance = new Singleton();
	}
	
	public static Singleton getInstance() {
		return SingletonInnerClass.instance;//SingletonInnerClass is loaded once
	}
}
```

### 8. 枚举
```java
public enum Singleton {
	INSTANCE;
	public void sayOK(){
	}
}
```
