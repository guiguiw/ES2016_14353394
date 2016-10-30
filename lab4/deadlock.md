#死锁

##基本概念##
死锁：两个或多个进程无限地等待一个事件，而该事件只能由这些等待进程之一来产生。  
死锁的四个必要条件：  
  
- 互斥：至少有一个资源必须处于非共享的模式，即一次只有一个进程使用，如果另一个进程申请该资源，那么申请进程必须等到该资源被释放为止。
- 占有并等待：一个进程必须占有至少一个资源，并等待另一个资源，而该资源为其他进程锁所占有。
- 非抢占：资源不可被抢占，资源只能在进程完成后释放。
- 循环等待：若干进程之间形成一种头尾相接的循环等待资源关系  
  
我们可以利用下图对死锁做个形象的解释：  

![](http://i1.piimg.com/567571/4e4d0e5a56568ca2.png)  
  
  
如图所示，T1进程正在使用资源R1，同时T1也在申请R2资源，而R2资源被T2进程所占有，T2进程同时也在申请被T1所占有的R1资源。此时这两个进程进入死锁状态，都在等待对方释放所占有资源，进入循环等待。  
  
##实验代码分析##
首先贴出源代码：  

    class A{
	     synchronized void methodA(B b){
		 b.last();
	       }
	
	synchronized void last(){
		System.out.println("Inside A.last()");
	    }

    }

    class B{
	    synchronized void methodB(A a){
		a.last();
	    }
	
	synchronized void last(){
		System.out.println("Inside B.last()");
	    }
    }

    class Deadlock implements Runnable{
	    A a=new A();
	    B b=new B();
       //构造函数
	   Deadlock(){
		   Thread t = new Thread(this);
		   int count = 10000;
		
		   t.start();//线程t开始
		   while(count-->0);//等待10000
		   a.methodA(b);
	       }
       //runable运行时调用的方法
	   public void run(){
		   b.methodB(a);
	       }
	
	   public static void main(String args[]){
		  new Deadlock();
	       }
      }
  
分析：代码中使用了synchronized关键字，用它来修饰一个代码块时，能够保证在同一时刻只有一个线程执行该段代码，即其他想要调用该代码块的进程将被阻塞。  
接着分析发生死锁的情况：当线程t开始之后，会被放入到调度队列，等待调度；当被调度时，就会运行run函数的内容，第一次会调用classB的内容，随后在一段时间后，会接着调用classA中的内容；若要达到死锁，则需要两个进程的运行时间和等待时间恰好满足死锁的必要条件。这样就会发生死锁。 
  
##测试死锁代码实现情况##
在Ubuntu中写一个运行脚本，让死锁的代码循环100次，以下是代码：
    
    for c in `seq 100`
    do
       echo "$c times"
       java Deadlock
    done
接着在终端运行该文件，在死锁时会停下来；  
成功死锁时的截图：  
![](http://i1.piimg.com/567571/c67d716cd92a47ee.png)   

如果出现无法死锁的情况，则需要改变count的值，由于死锁是随机的，所以需要耐心调试和等待。