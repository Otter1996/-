# C#基本架構
1. C#是一種強型別語言，變數要使用必須先進行型別宣告。每一種型別(type)代表各種不同邏輯結構，例如:檔案系統、網路連接、物件的集合和陣列，以及日期。一般C#程式會使用類別庫(Library)和使用者自訂義型別來建立程式問題領域概念的專屬模型。
2. C#內建許多型別(type)供使用，每一種型別皆儲存不同種的資料。例如:int可以儲存整數、double可以儲存浮點數...。而每一種型別皆有專屬的MetaData。
3. MSDN解釋MetaData(中繼資料)裡儲存的東西有:
    1. 型別變數需要的儲存空間。
    2. 它可以代表的最大值和最小值
    3. 它所包含的成員(方法、欄位、事件...等等)
    4. 它所繼承的基底型別
    5. 允許的作業類型
    6. 它所執行的介面
4. MSDN把型別分群:分成內建型別、自訂型別。
    1. 內建型別-ValueType: bool、byte、int、long、short...等等
    2. 內建型別-ReferenceType: object、string、dynamic
    3. 自訂型別-ValueType: enum、struct...
    4. 自訂型別-ReferenceType: class、Interface...
    ![](https://i.imgur.com/sK2S8Vu.png)
    ![](https://i.imgur.com/QCPoVHp.png)

5. .NET類別庫本身就是一個巨大的自訂類型集合。但必須將專案參考新增至其定義所在的元件時專案才可以使用

6. C#編譯過程縮略圖![](https://i.imgur.com/qKEyVNj.png)
    1. 一般型別系統(CTS:Common Type System):是屬於.NET中的型別系統，有兩個基本要點
    (1) 它支持繼承原則，分成衍生型別和基底型別。衍生型別會繼承基底型別的方法、屬性、和其他成員。所有型別(包括Int、class、Interface、delegate)最終都是從單一基底型別衍生而來，這殼基底型別是"object"(System.Object)。
    (2) CTS中的每個型別都會定義【實質型別(valueType)】和【參考型別(referenceType)】。如果任何型別有繼承strcut型別，那就一定是valueType；如果是class型別或是record型別那就是referenceType。
    (3) 對編譯器(compiler)來說ValueTyp、RefType都有各自的編譯原則和不同runtime行為。
    (4) CTS定義了一套通用的編譯時的數據型別系統。舉一個簡單的例子在vb.net中對整數的定義為integer；在C#中對整數的定義為int，在編譯之後interger和int統一變為Int32
    ![](https://i.imgur.com/qkk9Py3.png)
    2. IL(中間語言):是由CLS(Common Language Specification)編譯，實現通用，反編譯就可以形成其他代碼。在.net framework有二次編譯的概念，二次編譯，為了不同平台上使用，加上一層中間層，更靈活，透過VS編譯器　編譯成dll/exe，點擊exe的時候，他有一個依賴的環境叫做CLR，dll/exe裡面包含兩大塊:IL（中間語言）和metadata(中繼資料)。metadata會紀錄這dll/exe裡面有哪些東西
    3. CLR(Common Language Runtime):用於驅動程式運行，執行及時編譯(JIT:Just in time)，將IL代碼轉換成機器指令。另外還包括垃圾回收(GC:Garbage Collection)等。
7. 待新增..........
