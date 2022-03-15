### What are the wait() and sleep() methods?
wait(): As the name suggests, it is a non-static method that causes the current thread to wait and go to sleep until some other threads call the notify () or notifyAll() method for the object’s monitor (lock). It simply releases the lock and is mostly used for inter-thread communication. It is defined in the object class, and should only be called from a synchronized context. 

Example:  

synchronized(monitor) 
{ 
monitor.wait();       Here Lock Is Released by Current Thread  
} 
sleep(): As the name suggests, it is a static method that pauses or stops the execution of the current thread for some specified period. It doesn’t release the lock while waiting and is mostly used to introduce pause on execution. It is defined in thread class, and no need to call from a synchronized context.  

Example:  

synchronized(monitor) 
{ 
Thread.sleep(1000);     Here Lock Is Held by The Current Thread 
//after 1000 milliseconds, the current thread will wake up, or after we call that is interrupt() method 
}

### What’s the difference between notify() and notifyAll()?
notify(): It sends a notification and wakes up only a single thread instead of multiple threads that are waiting on the object’s monitor.
![image](https://user-images.githubusercontent.com/100063114/158354237-67743d07-db25-4a31-a219-8e8ed0f234da.png)

notifyAll(): It sends notifications and wakes up all threads and allows them to compete for the object's monitor instead of a single thread.

![image](https://user-images.githubusercontent.com/100063114/158354275-30b2cf09-6cf3-4201-a3fb-057608fbf856.png)

### Why wait(), notify(), and notifyAll() methods are present in Object class?
- Object has monitors.
- Multiple threads can access one Object. Only one thread can hold object monitor at a time for synchronized methods/blocks.
- wait(), notify() and notifyAll() method being in Object class allows all the threads created on that object to communicate with other
- Locking ( using synchronized or Lock API) and Communication (wait() and notify()) are two different concepts.

If Thread class contains wait(), notify() and notifyAll() methods, then it will create below problems:

- Thread communication problem
- Synchronization on object won’t be possible. If each thread will have monitor, we won’t have any way of achieving synchronization
- Inconsistency in state of object

### What is Runnable and Callable Interface? Write the difference between them.
Both the interfaces are generally used to encapsulate tasks that are needed to be executed by another thread. But there are some differences between them as given below: 

- Running Interface: This interface is basically available in Java right from the beginning. It is simply used to execute code on a concurrent thread.  
- Callable Interface: This interface is basically a new one that was introduced as a part of the concurrency package. It addresses the limitation of runnable interfaces along with some major changes like generics, enum, static imports, variable argument method, etc. It uses generics to define the return type of object.   
~~~
public interface Runnable  
{   
  public abstract void run(); 
}  
public interface Callable<V>  
{    
V call() throws Exception;  
} 
~~~

### Explain thread pool?
A Thread pool is simply a collection of pre-initialized or worker threads at the start-up that can be used to execute tasks and put back in the pool when completed. It is referred to as pool threads in which a group of fixed-size threads is created.  By reducing the number of application threads and managing their lifecycle, one can mitigate the issue of performance using a thread pool. Using threads, performance can be enhanced and better system stability can occur. To create the thread pools, java.util.concurrent.Executors class usually provides factory methods.

### What’s the purpose of the join() method?
join() method is generally used to pause the execution of a current thread unless and until the specified thread on which join is called is dead or completed. To stop a thread from running until another thread gets ended, this method can be used. It joins the start of a thread execution to the end of another thread’s execution. It is considered the final method of a thread class.

### What do you mean by garbage collection?
Garbage collection is basically a process of managing memory automatically. It uses several GC algorithms among which the popular one includes Mark and Sweep. The process includes three phases i.e., marking, deletion, and compaction/copying. In simple words, a garbage collector finds objects that are no longer required by the program and then delete or remove these unused objects to free up the memory space.

### Explain the meaning of the deadlock and when it can occur?
Deadlock, as the name suggests, is a situation where multiple threads are blocked forever. It generally occurs when multiple threads hold locks on different resources and are waiting for other resources to complete their task.
![image](https://user-images.githubusercontent.com/100063114/158355146-1355696a-260d-4a9e-8654-54f523ba0976.png)


The above diagram shows a deadlock situation where two threads are blocked forever.  Thread 1 is holding Object 1 but needs object 2 to complete processing whereas Thread 2 is holding Object 2 but needs object 1 first. In such conditions, both of them will hold lock forever and will never complete tasks.
~~~
public class TestDeadlockExample1 {  
  public static void main(String[] args) {  
    final String resource1 = "ratan jaiswal";  
    final String resource2 = "vimal jaiswal";  
    // t1 tries to lock resource1 then resource2  
    Thread t1 = new Thread() {  
      public void run() {  
          synchronized (resource1) {  
           System.out.println("Thread 1: locked resource 1");  
  
           try { Thread.sleep(100);} catch (Exception e) {}  
  
           synchronized (resource2) {  
            System.out.println("Thread 1: locked resource 2");  
           }  
         }  
      }  
    };  
  
    // t2 tries to lock resource2 then resource1  
    Thread t2 = new Thread() {  
      public void run() {  
        synchronized (resource2) {  
          System.out.println("Thread 2: locked resource 2");  
  
          try { Thread.sleep(100);} catch (Exception e) {}  
  
          synchronized (resource1) {  
            System.out.println("Thread 2: locked resource 1");  
          }  
        }  
      }  
    };  
  
      
    t1.start();  
    t2.start();  
  }  
}     
~~~
### Explain volatile variables in Java?
A volatile variable is basically a keyword that is used to ensure and address the visibility of changes to variables in multithreaded programming. This keyword cannot be used with classes and methods, instead can be used with variables. It is simply used to achieve thread-safety. If you mark any variable as volatile, then all the threads can read its value directly from the main memory rather than CPU cache, so that each thread can get an updated value of the variable.

### How do threads communicate with each other?
Threads can communicate using three methods i.e., wait(), notify(), and notifyAll()

