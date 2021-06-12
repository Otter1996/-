# C#委託(delegate)
1. 委託是C#的特殊型別，能夠持有其他類別裡一個或多個方法的【方法】，並且該方法還可以將我們自己的方法當成參數，傳到另一個方法來跑。
2. 這種將方法動態地賦給引數的作法，可以避免在程式中【大量使用if-else、switch語句】，同時使得程式具有更好的可擴充性。
3. 委託的條件:輸入參數的資料型態+輸出資料型態一樣就能符合委託的條件。舉例:
```
//宣告delegate型別，輸入的參數為字串name，輸出的參數為int。InStrOutInt為委派方法
delegate int InStrOutInt(string name);

//方法GetHight，由於符合輸出輸入的條件，故可以使用InStrOutInt委派型別的方法
static int GetHeight(string name){return 180;}

//同上
static int GetWeight(string name)
{return 70;]}
```
4. 要引用(註冊)委派，可以**實力化**一委派型別，並把符合該委派類別條件的方法放入參數。舉例:
```
//正確(O)
InStrOutInt a = new InsStrOutInt(GetHeight);

//直接寫註冊委託的方法，也正確(O)
InStrOutInt a = GetHeight;
```
這時候a為InStrOutInt的變數，所以委託方法InStrOutInt夾帶著方法給其他方法使用。
```
static void main(string args[])
{
    InStrOutInt a = new InStrOutInt(GetHeight);
    Int message = a("Tom");
    //output:180;
    Console.WriteLine(message);
}
```
5. 當一個委託沒有指向任何一個方法的時候，此用該委託就會出現異常並回傳null報錯。
6. 委派的好處:
使用委派可以一次做好幾個工作，工作內容可以自行增減，這叫做多重委派(大陸稱:多播委託)
    ```
    static void Test1()
    {
        console.WriteLine("Test1");
    }
    static void Test2()
    {
        console.WriteLine("Test2");
    }
    public static void Main(string[] args)
    {
        action a = test1; //註冊test1到action a變數
        a += test2; //註冊test2到a變數
        a();
        console.Writeline(a);
        //output:Test1Test2
    ]
    ```
7. 多重委派裡有一個常見的方法為GetInvocationList()方法，可以取出委託裡所有已經註冊的方法，返回值為Delegate[]型別陣列。並可以使用foreach遍歷多重委派中的所有委託並單獨調用。
8. 委派的方式有三種:
    1. 具名方法:
    ```
    static void Main (string[] args) {
    MyDelegate d;

    d = new MyDelegate (add);
    var v = d (1, 2); // 1 + 2 = 3
    Console.WriteLine (v);

    d = new MyDelegate (subtract);
    v = d (2, 1); // 2 - 1 = 1
    Console.WriteLine (v);
    }
    public delegate int MyDelegate (int x, int y);

    public static int add (int a, int b) {
      return a + b;
    }
    public static int subtract (int a, int b) {
    return a - b;
    }

    ```
    3. 匿名方法:使用匿名方法可以減少在具現化委派中撰寫程式碼的額外負荷，因為不必另外建立一個方法並將此方法傳入delegate中。直接就可以寫入方法輸入參數和輸出。
    ```
    public delegate int MyDelegate (int x, int y);

    static void Main (string[] args) {
      MyDelegate d; //初始化
      d = delegate (int x, int y) {
        return x + y;
      };
      var v = d (1, 2); // 1 + 2 = 3
      Console.WriteLine (v);
      d = delegate (int x, int y) {
        return x - y;
      };
      v = d (2, 1); // 2 - 1 = 1
      Console.WriteLine (v);
    }
    ```
    5. Lambda表達式:以lambda運算式取代匿名方法，成為撰寫程式碼內嵌的【慣用方式】
    ```
    public delegate int MyDelegate (int x, int y);
    
    static void Main (string[] args) {
      MyDelegate d;
      d = (int x, int y) => { return x + y; };
      var v = d (1, 2); // 1 + 2 = 3
      Console.WriteLine (v);
      d = (x, y) => x - y;
      v = d (2, 1); // 2 - 1 = 1
      Console.WriteLine (v);
    }
    ```
9. 除了delegate，也可以使用Action、Func、Predicate這些型別來進行委派，最大的特色是不用事先宣告委派的型別!
    1. Action:Action是無傳回值的泛型委派。至少輸入0個參數，至多16個。舉例:
    ```
    static void Main (string[] args) { 
      Action<string> action = action1; /*其中<string>代表的是要輸入的資料格式*/
      action ("123"); // 123
      action = action2;
      action ("Mio"); // Hi Mio
    }
    public static void action1 (string a) {
      Console.WriteLine (a);
    }
    public static void action2 (string a) {
      Console.WriteLine ("Hi " + a);
    }

    ```
    2. Func:Func是有傳回值的泛型委派。至少要有0個參數，至多16個，【以及一個傳回值的型別參數】。方法必須有傳回值，不可以為void。</br>
        (1)格式:Func<輸入值，輸入值，...，輸出值>，意思是Func泛型參數寫在前面都是輸入參數，只有最後一個為輸出值。舉例:
        ```
        static void main(string[] args)        {    
        Func<int> func = func1;//宣告func變數為Func<int>型別，無輸入值，輸出值為int
        Console.WriteLine(func()); //output:0
        }
        public static int func1()
        {
            return 0;
        }
        ```
        </br>
        (2)使用Func委派時，也能用Lambda進行。
        ```
        static void Main(string args){
            Func<int> func = ()=>0;
            Console.WriteLine(func()); //output:0
            Func<int,int,string> func2 =(a,b)=>(a+b).ToString();
            Console.WriteLine(func2(1,2)); //output:1+2=3
        
        }
        ```
        </br>
    3. Predicate:Predicate是返回bool型別的泛型委派。`Predicate<int>`表示傳入參數為int返回bool的委派。Predicate有且只有一個參數，傳回值固定為bool。舉例:
    ```
    static void Main (string[] args) {
      Predicate<int> predicate = predicate1;
      Console.WriteLine (predicate (0)); // True
    }
    public static bool predicate1 (int a) {
      return a == 0;
    }

    ```
10. Delegate的CallBack方法:
     
        

    
    