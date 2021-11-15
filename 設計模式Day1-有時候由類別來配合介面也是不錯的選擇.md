設計模式 思路
1.如果繼承的類別中有不要的function該怎麼辦 -> override它使其內部function為空(X) -> 不要把該function放入父類別，使用介面替代(X) ->使用設計模式思路:找出程式中可能需要更動之處，把它們獨立出來，不要和那些不需要的混雜在一起，更明確的說就是把會變動的部分取出並【封裝】起來，好讓其他部分不會受到影響。再這期間會使用到介面去指向實作某方法的類別。P.17

```
public class Main
{
	public static void main(String[] args) {
		MallardDuck duck1 = new MallardDuck();
		duck1.swim();
		duck1.display();
		duck1.performFly();
		duck1.performquack();
	}
}

abstract class Duck
{
    IFlyBehavior flybehavior;
    IQuackBehavior quackbehavior;
    
    public void swim(){
        System.out.println("I am swimming");
    }
    
    public abstract void display();
    
    public void performFly(){
        flybehavior.fly();
    }
    public void performquack(){
        quackbehavior.quack();
    }
}

class MallardDuck extends Duck
{
    public MallardDuck()
    {
        flybehavior = new FlyNoWay();
        quackbehavior = new Quack();
    }
    
    public void display()
    {
        System.out.println("I am MallarDuck");
    }
}

interface IFlyBehavior{
    public void fly();
}

interface IQuackBehavior{
    public void quack();
}

class Flywithwings implements IFlyBehavior{
    public void fly(){
        System.out.println("I am Flying");
    }
}
class FlyNoWay implements IFlyBehavior{
    public void fly(){
        System.out.println("I can't fly");
    }
}
class Quack implements IQuackBehavior{
    public void quack(){
        System.out.println("quack quack quack");
    }
}
class MuteQuack implements IQuackBehavior{
    public void quack(){
        System.out.println("No sound");
    }
}
class Squack implements IQuackBehavior{
    public void quack(){
        System.out.println("sqauck squack squack");
    }
}

```