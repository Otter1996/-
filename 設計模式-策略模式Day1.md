# 設計模式-策略模式
## 假設情境:
今天團隊要開發鴨子模組，總共有一百種不同的鴨子，每隻鴨子都會游泳，但是有些鴨子會飛有些不會飛，有些會叫有些不會叫。有些鴨子叫聲是聒聒、有些是嘎嘎，還有一些是不會叫的鴨子。這時候能怎麼設計?

## 剛上大學的我
如果假設今天是剛上大學還不懂OO的人，可能會設定一個Superclass(超類別、父類別)再加上好幾個Subclass(副類別、子類別)。會變成這樣子設計:
```
abstract class Duck
{
    public void swim(){
        //Write Some Code
    }
    public abstract void Fly(){}
    public abstract void Quack(){}
}

class Duck_A : Duck
{
    public override void Fly()
    {
        Console.WriteLine("我會飛");
    }
    public override void Quack()
    {
        Console.WriteLine("聒聒");
    }
}

class Duck_B : Duck
{
  public override void Fly()
    {
        Console.WriteLine("我不會飛");
    }
    public override void Quack()
    {
        Console.WriteLine("...");
    }  
}
```
你可能會覺得，耶?看起來沒什麼問題啊?但是再多思考一下，當你今天不需要鴨子叫的時候，你仍然需要override Quack這個方法(如果不Override就會報錯，原因是未實作抽象成員。)如果有25種鴨子不會叫，你就必須重複多打25次無意義的方法，這實在是很不聰明的事。
你又會說，那不要abstract就好了，這樣也不會報錯。那這樣你的理解就錯了，當今天老闆要替【鴨子】這個超類別，新增個功能，假設是"大便"方法好了，一新增下去，所有繼承鴨子的subclss都會繼承"大便"這個方法，卻沒注意到連塑膠鴨子都繼承了。現在可好了，你的程式的塑膠鴨子會大便。

## 剛出社會的我
我學會了基本的OO之後，我還覺得自己很帥的用了Interface的用法就算是優雅的解決這個問題。
```
abstract class Duck
{
    public void swim(){
        //Write Some Code
    }
}

public Interface IFlyable
{
    void Fly();
}

public Interface IQuackable
{
    void Quack();
}

class Duck_A : Duck,IFlyable,IQuackable
{
    public override void Fly()
    {
        Console.WriteLine("我會飛");
    }
    public override void Quack()
    {
        Console.WriteLine("聒聒");
    }
}

class Duck_B : Duck,IFlyable
{
  public override void Fly()
    {
        Console.WriteLine("我會飛");
    }
}
```
如此一來IDE就不會報錯啦!因為我把【飛】跟【叫】這個兩方法，獨自定義在自己的Interface裡。只要鴨子會飛就插入IFlyable、會叫就插入IQuackable。但是假設今天老闆要將【所有的聒聒叫法】改成【呱呱】，那這時候就頭大了，你所有有實作IQauckable的鴨子都要挑出來，"一個一個"修改。100隻還好，1W隻你會就哭出來了。這也是我為什麼要去讀設計模式的原因...，我們來看一下，大師們怎麼寫出有彈性的架構。

## 策略模式
```
abstract class Duck
{
    //宣告flyBehavior變數，其型別為IFlyable
    public IFlyable flyBehavior;
    //同上
    public IQuackable quackBehavior;
    //所有鴨子都會游泳
    public void swim()
    {
        Console.WriteLine("我游泳可是很厲害的喔!")
    }
    public void Fly()
    {    //執行flyBehavior這個物件所【指向】的實例的fly方法
        flyBehavior.fly(); 
    }
    public void Quack()
    {   //執行quackBehavior這個物件所【指向】的實例的fly方法
        quackBehavior.quack();
    }
}
-----------------------------------------------------------
public Interface IFlyable
{
    void Fly();
}

public Interface IQuackable
{
    void Quack();
}
----------------------------------------------------------
//創一新類別其實作介面IFlyable
class FlyWithWings :IFlyable 
{
    public void fly()
    {
        Console.WriteLine("我可以飛!");
    }
}
//同上
class FlyNoWay : IFlyable 
{
    public void fly() 
    {
        Console.WriteLine("我不會飛!");
    }
}
//同上
class Quack : IQuackable
{
    public void quack() 
    {
        Console.WriteLine("聒聒");
    }
}
//同上
class Squeak : IQuackable
{
    public void quack() 
    {
        Console.WriteLine("嘎嘎");
    }
}
//同上
class MuteQuack : IQuackable
{
    public void quack()
    {
        Console.WriteLine("....");
    }
}
//同上
class BossQuack : IQuackable
{
    public void quack()
    {
        Console.WriteLine("呱呱");
    }
}
```
好這時候我們來設計一隻鴨子，不會飛、會叫(叫聲是老闆要求新增的)。
```
class MallardDuck : Duck
{
    //建構子
    public MallardDuck()
    {
        //將類別FlyWithWing
        flyBehavior = new FlyWithWings();
        quackBehavior = new BossQuack();
    }
}
class Program
{
    static void Main(string[] args)
    {
        MallardDuck mallard = new MallardDuck();
        mallard.Fly();
        mallard.Quack();
        mallard.swim();
        Console.ReadLine();
        
        /*
        output:
        我可以飛!
        呱呱
        我游泳可是很厲害的喔!
        */
        
    }
}

```
## 小結:
設計模式真的是所有軟工師都要拜讀的一本書，跟演算法一樣都是前人所走過來的心血。愧於我太晚頓悟，才多走了那麼多的冤枉路。