# 8.8test

一、选择题(20题，每题2分，共20分)

1. 在Java中，以下代码( A  )正确地创建了一个InputStreamReader对象。
A.  InuptStreamReader(new FileInputStream(“1.dat”));
B.  InuptStreamReader(new FileReader(“1.dat”));
C.  InuptStreamReader(new BufferReader(“1.dat”));
D.  InuptStreamReader (“1.dat”);

2. 根据下面的代码，
String s = null;
会抛出NullPointerException异常的有（ AC）。[两项]
A.  if( (s!=null) & (s.length()>0) )
B.  if( (s!=null) & & (s.length()>0) )
C.  if( (s==null) | (s.length()==0) )
D.  if( (s==null) || (s.length()==0) )

3． 以下代码运行输出是（C ）
public class Person{
  private String name=”Person”;
  int age=0;
}
public class Child extends Person{
  public String grade;
  public static void main(String[] args){
  Person p = new Child();
  System.out.println(p.name);
}
}
A. 输出：Person
B. 没有输出
C. 编译出错
D. 运行出错

4.ArrayList list = new ArrayList(20);中的 list 扩容( A )次 
//扩容前提 ：数据存满了，扩容
A. 0 
B. 1 
C. 2 
D. 3

5.有以下方法的定义，请选择该方法的返回类型（ D）
	ReturnType method(byte x,double y){
		 return (short)x/y*2;
}
A.Byte
B.Short
C.Int
D.Double

6. 在Java中，(A )类可用于创建链表数据结构的对象
A.  LinkedList
B.  ArrayList
C.  Collection
D.  HashMap

7. 在Java中，关于HashMap类的描述，以下描述错误的是( B )
A.  HashMap使用键/值得形式保存数据
B.  HashMap 能够保证其中元素的顺序
C.  HashMap允许将null用作键
D.  HashMap允许将null用作值

8． 在try-catch-finally语句块中，以下可以单独与finally一起使用的是（B ）
A.  catch
B.  try
C.  throws
D.  throw

9． 接口和抽象类描述正确的有（BC ）（两项）
A.  抽象类没有构造函数
B.  接口没有构造函数
C.  抽象类不允许多继承
D.  接口中的方法可以有方法体

10． 在使用super 和this关键字时，以下描述正确的是（ A）
A.  在子类构造方法中使用super（）显示调用父类的构造方法，super（）必须写在子类构造方法的第一行，否则编译不通过
B.  super（）和this（）不一定要放在构造方法内第一行
C.  this（）和super（）可以同时出现在一个构造函数中
D. this（）和super（）可以在static环境中使用，包括static方法和static语句块

二、简答题（5题，每题6分，共30分）

	评分标准：回答出关键点可以酌情给分！！

1．Java访问修饰符有哪些？各个访问修饰符的作用范围是什么？
private  package（default）默认的  protected public
private：只能在当前类使用
默认的：当前类，或者同一个包下面的类
Protected：当前类，或者同一个包下面的类，子类中可以使用
Public：任何类中

2.	简述String 和 StringBuilder以及StringBuffer的区别
   String:不变性
StringBuffer和StringBuilder具有可变性
StringBuffer线程安全，效率低
StringBuilder线程不安全，效率较高

3.	简述Overload-重载 和 Override-重写 的区别
重载：发生一个类中、方法名相同、参数列表不同（参数数据类型不同、个数不同、顺序不同） 返回值类型和访问修饰符不作为判断重载的依据


重写：发生父子类中，方法名相同、参数列表相同、返回值类型相同。
子类重写父类方法，访问修饰符范围不能小于父类

4. 接口是否可继承接口? 抽象类是否可实现(implements)接口? 抽象类是否可继承 实体类(concrete class)?  抽象类中是否可以有静态的 main 方法？

都是可以的。

5. List与Map的差别
List：只能单列存储。有序、可以重复

Map：键值对存储、hashMap 无序、键不允许重复


三、机试题（5题，每题10分，共50分）

评分标准：能够实现效果即可得分

1、任意定义20个字母，输出出现次数最多的字母和次数 

String str="hfhghgfhgfhghddgghh";

参考答案：
public static void main(String[] args) {
        String str="hfhghgfhgfhghddgghh";
        Map map=new HashMap();//这个map中 key是组成str的每个字符(a,b,c,1),value是字符出现的次数
        
        for (int i = 0; i < str.length(); i++) {//循环str字符串
            String s=str.substring(i,i+1);//取出一个字符串
            if (map.containsKey(s)) {//如果这个字符作为key在map已存在
                int value=Integer.parseInt(map.get(s).toString());//获取对应的value并转换为int
                map.remove(s);//删除map中的这列数据
                map.put(s, value+1);//重新加入新的一列数据,key为字符,value为以前的value+1
            }else {
                map.put(s, 1);//如果不存在直接添加进去,并且value为1
            }
        }
        
        //System.out.println("map的长度: "+map.size());
        int maxValue=0;//存储最大value
        String maxKey="";//存储最大key
        for(Object o :map.entrySet()){
        	//遍历这个map,并获取具有最大值的map对象的key与value放入以上两个变量(类似于冒泡排序)
            Map.Entry me=(Entry) o;
            String key=me.getKey().toString();
            int value=Integer.parseInt(me.getValue().toString());
            if(value>maxValue){
                maxValue=value;
                maxKey=key;
            }
        }
        System.out.println("出现最多的是: "+maxKey +" 总共出现了: "+maxValue+"次");//输出结果
    }


4.有一个字符串"woaijavahajajavavahajavaaiwo"删除该字符串中所有的"java"并且统计删除了多少个“java”
将删除完的字符串和删除个数在控制台打印出来

参考答案：
public static void main(String[] args) {
        String strone = "woaijavahajajavavahajavaaiwo";
        String strjava = "java";
        int index = 0;
        int count=0;
        //记录第一次出现java的位置,直到没有结束循环
        while((index = strone.indexOf(strjava))!=-1){
            //把出现成java的字符串给去除掉
            strone = strone.substring(0,index).concat(strone.substring(index+strjava.length()));
            count++;
        }
        System.out.println(strone);
        System.out.println(count);
    }
