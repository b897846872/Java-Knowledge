## 线程状态
6个状态定义：java.lang.Thread.State
1. New（新线程）：尚未启动的线程的线程状态。
2. Runnable（可运行状态）：可运行线程的线程状态，等待CPU调度。
3. Bocked（阻塞状态）：线程阻塞等待监视器锁定的线程状态。处于synchronized同步代码块或方法中被阻塞。
4. Waiting（等待状态）：等待线程的线程状态。
5. Timed Waiting（定时等待）：具有指定等待时间的等待线程的线程状态。
6. Terminated（终止）：线程执行结束。

## 创建线程
1.继承Java.lang.Thread类，重写run方法：
```java
public class ThreadCreate2 extends Thread{
	@Override
	public void run() {
		System.out.println(333);
	}

	public static void main(String[] args) {
		new ThreadCreate2().start();
	}
}
```
2.实现Runnable类，重写run方法：
```java
public class ThreadCreate1 implements Runnable{
	@Override
	public void run() {
		System.out.println(2);
	}
	
	public static void main(String[] args) {
		ThreadCreate1 thread1= new ThreadCreate1();
		Thread thread2 = new Thread(thread1);
		thread2.start();
	}
}
```
3.Java不支持类的多重继承，但允许你调用多个接口。所以如果你要继承其他类，当然是调用Runnable接口好了。
## Thread的start()和run()函数区别
1.start()方法来启动线程，真正实现了多线程运行，这时无需等待
run方法体代码执行完毕而直接继续执行下面的代码： 通过调用Thread类的start()方法来启动一个线程，这时此线程是处于就绪状态，并没有运行。然后通过
此Thread类调用方法run()来完成其运行操作的，这里方法run()称为线程体，它包含了要执行的这个线程的内容，Run方法运行结束，此线程终止，而CPU再运行其它线程。

2.run()方法当作普通方法的方式调用，程序还是要顺序执行，还是要等待run方法体执行完毕后才可继续执行下面的代码： 而如果直接用run
方法，这只是调用一个方法而已，程序中依然只有主线程--这一个线程，其程序执行路径还是只有一条，这样就没有达到写线程的目的。

总结：调用start方法方可启动线程，而run方法只是thread的一个普通方法调用，还是在主线程里执行。这两个方法应该都比较熟悉，把需要并行处理的代码放在run()方法中，start()方法启动线程将自动调用 run()方法，这是由jvm的内存机制规定的。并且run()方法必须是public访问权限，返回值类型为void。

## volatile与synchronized 的比较
volatile主要用在多个线程感知实例变量被更改了场合，从而使得各个线程获得最新的值。它强制线程每次从主内存中讲到变量，而不是从线程的私有内存中读取变量，从而保证了数据的可见性。
1. volatile轻量级，只能修饰变量。synchronized重量级，还可修饰方法；
2. volatile只能保证数据的可见性，不能用来同步，因为多个线程并发访问volatile修饰的变量不会阻塞；
synchronized不仅保证可见性，而且还保证原子性，因为，只有获得了锁的线程才能进入临界区，从而保证临界区中的所有语句都全部执行。多个线程争抢synchronized锁对象时，会出现阻塞。

## wait和notify
1. wait( )，notify( )，notifyAll( )都不属于Thread类，而是属于Object基础类，也就是每个对象都有wait( )，notify( )，notifyAll( ) 的功能，因为每个对象都有锁，锁是每个对象的基础，当然操作锁的方法也是最基础了。
2. 当需要调用以上的方法的时候，一定要对竞争资源进行加锁，如果不加锁的话，则会报 IllegalMonitorStateException 异常。
3. notify( )方法只会通知等待队列中的第一个相关线程（不会通知优先级比较高的线程）；notifyAll( )通知所有等待该竞争资源的线程（也不会按照线程的优先级来执行）。

## synchronized与Lock的区别
1. 首先synchronized是java内置关键字，在jvm层面，Lock是个java类；
2. synchronized无法判断是否获取锁的状态，Lock可以判断是否获取到锁；
3. synchronized会自动释放锁(a 线程执行完同步代码会释放锁 ；b 线程执行过程中发生异常会释放锁)，Lock需在finally中手工释放锁（unlock()方法释放锁），否则容易造成线程死锁；
4. 用synchronized关键字的两个线程1和线程2，如果当前线程1获得锁，线程2线程等待。如果线程1阻塞，线程2则会一直等待下去，而Lock锁就不一定会等待下去，如果尝试获取不到锁，线程可以不用一直等待就结束了；
5. synchronized的锁可重入、不可中断、非公平，而Lock锁可重入、可判断、可公平（两者皆可）
6. Lock锁适合大量同步的代码的同步问题，synchronized锁适合代码少量的同步问题。

## 线程本地变量ThreadLocal
1. 并发应用的一个关键地方就是共享数据。如果你创建一个类对象，实现Runnable接口，然后多个Thread对象使用同样的Runnable对象，全部的线程都共享同样的属性。这意味着，如果你在一个线程里改变一个属性，全部的线程都会受到这个改变的影响。
有时，你希望程序里的各个线程的属性不会被共享。 Java 并发 API提供了一个很清楚的机制叫本地线程变量即**ThreadLocal**。
模拟ThreadLocal类实现：线程范围内的共享变量，每个线程只能访问他自己的，不能访问别的线程。
2. 对于多线程资源共享的问题，同步机制(Synchronized)采用了“以时间换空间”的方式，
  而ThreadLocal采用了“以空间换时间”的方式。前者仅提供一份变量，让不同的线程排队访问，而后者为每一个线程都提供了一份变量，因此可以同时访问而互不影响。

## 堆和栈
每个线程都有自己的栈内存，用于存储本地变量，方法参数和栈 调用，一个线程中存储的变量对其它线程是不可见的。而堆是所有线程共享的一片公用内存区域。对象都在堆里创建，为了提升效率线程会从堆中弄一个缓存到自己 的栈，如果多个线程使用该变量就可能引发问题，这时volatile 变量就可以发挥作用了，它要求线程从主存中读取变量的值。

## sleep()和wait()
**共同点** ： 
1. 他们都是在多线程的环境下，都可以在程序的调用处阻塞指定的毫秒数，并返回。 
2. wait()和sleep()都可以通过interrupt()方法 打断线程的暂停状态 ，从而使线程立刻抛出InterruptedException。 
如果线程A希望立即结束线程B，则可以对线程B对应的Thread实例调用interrupt方法。如果此刻线程B正在wait/sleep/join，则线程B会立刻抛出InterruptedException，在catch() {} 中直接return即可安全地结束线程。 
需要注意的是，InterruptedException是线程自己从内部抛出的，并不是interrupt()方法抛出的。对某一线程调用 interrupt()时，如果该线程正在执行普通的代码，那么该线程根本就不会抛出InterruptedException。但是，一旦该线程进入到 wait()/sleep()/join()后，就会立刻抛出InterruptedException 。 
**不同点 **：  
1. 每个对象都有一个锁来控制同步访问。Synchronized关键字可以和对象的锁交互，来实现线程的同步。 
sleep方法没有释放锁，而wait方法释放了锁，使得其他线程可以使用同步控制块或者方法。 
2. wait，notify和notifyAll只能在同步控制方法或者同步控制块里面使用，而sleep可以在任何地方使用 
3. sleep必须捕获异常，而wait，notify和notifyAll不需要捕获异常 
4. sleep是线程类（Thread）的方法，导致此线程暂停执行指定时间，给执行机会给其他线程，但是监控状态依然保持，到时后会自动恢复。调用sleep不会释放对象锁。
5. wait是Object类的方法，对此对象调用wait方法导致本线程放弃对象锁，进入等待此对象的等待锁定池，只有针对此对象发出notify方法（或notifyAll）后本线程才进入对象锁定池准备获得对象锁进入运行状态。
