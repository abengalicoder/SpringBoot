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

### What is synchronized method and synchronized block? Which one should be preferred?
- Synchronized Method: In this method, the thread acquires a lock on the object when they enter the synchronized method and releases the lock either normally or by throwing an exception when they leave the method.  No other thread can use the whole method unless and until the current thread finishes its execution and release the lock. It can be used when one wants to lock on the entire functionality of a particular method. 

- Synchronized Block: In this method, the thread acquires a lock on the object between parentheses after the synchronized keyword, and releases the lock when they leave the block. No other thread can acquire a lock on the locked object unless and until the synchronized block exists. It can be used when one wants to keep other parts of the programs accessible to other threads.

### What is thread starvation?
Thread starvation is basically a situation or condition where a thread won’t be able to have regular access to shared resources and therefore is unable to proceed or make progress. This is because other threads have high priority and occupy the resources for too long. This usually happens with low-priority threads that do not get CPU for its execution to carry on. 
~~~
class StarvationDemo extends Thread {
    static int threadcount = 1;
    public void run()
    {
        System.out.println(threadcount + "st Child" +
                            " Thread execution starts");
        System.out.println("Child thread execution completes");
        threadcount++;
    }
    public static void main(String[] args)
               throws InterruptedException
    {
        System.out.println("Main thread execution starts");
 
        // Thread priorities are set in a way that thread5
        // gets least priority.
        StarvationDemo thread1 = new StarvationDemo();
        thread1.setPriority(10);
        StarvationDemo thread2 = new StarvationDemo();
        thread2.setPriority(9);
        StarvationDemo thread3 = new StarvationDemo();
        thread3.setPriority(8);
        StarvationDemo thread4 = new StarvationDemo();
        thread4.setPriority(7);
        StarvationDemo thread5 = new StarvationDemo();
        thread5.setPriority(6);
 
        thread1.start();
        thread2.start();
        thread3.start();
        thread4.start();
 
        // Here thread5 have to wait because of the
        // other thread. But after waiting for some
        // interval, thread5 will get the chance of
        // execution. It is known as Starvation
        thread5.start();
 
        System.out.println("Main thread execution completes");
    }
}
~~~

### What is BlockingQueue?
BlockingQueue basically represents a queue that is thread-safe. Producer thread inserts resource/element into the queue using put() method unless it gets full and consumer thread takes resources from the queue using take() method until it gets empty. But if a thread tries to dequeue from an empty queue, then a particular thread will be blocked until some other thread inserts an item into the queue, or if a thread tries to insert an item into a queue that is already full, then a particular thread will be blocked until some threads take away an item from the queue. 

### What Do You Understand By Executor Framework In Java?

Answer :

Executor Framework in java has been introduced in JDK 5. Executor Framework handles creation of thread, creating the thread pool and checking health while running and also terminates if needed.

### Question 2. What Is The Role Of Executorservice In Java?

Answer :

ExecutorService provides different methods to start and terminate thread. There are two methods execute() and submit() in ExecutorService. Execute() method is used for threads which is Runnable and submit() method is used for Callable threads.

### Question 3. What Is Executors In Java Executor Framework?

Answer :

Executors is a factory that provides the methods to return ExecutorService, ScheduledExecutorService, ThreadFactory. Find some method details. 

- newFixedThreadPool(): It returns the pool with fixed number of size. We need to pass the number of threads to this method. If concurrently task are submitted more than the pool size, then rest of task need to wait in queue. It returns ExecutorService. 

- newScheduledThreadPool: This also creates a fixed size pool but it can schedule the thread to run after some defined delay. It is useful to schedule the task. It returns ScheduledExecutorService. 

- newCachedThreadPool(): There is no fixed size of this pool. Thread will be created at run time and if there is no task it will alive for 60 second and then die. For short lived threads this pool works good. It returns ExecutorService.

### What Is The Role Of Futuretask And Future In Java?

Answer :

FutureTask is a cancellable asynchronous computation in java. It can cancel the task which is running. Once the FutureTask will be cancelled, it cannot be restarted. Future is result of asynchronous computation. Future checks if task is complete and if completed it gets the output.

### what is compleatable future

A CompltableFuture is used for asynchronous programming. Asynchronous programming means writing non-blocking code. It runs a task on a separate thread than the main application thread and notifies the main thread about its progress, completion or failure.

### CompletableFuture runAsync vs supplyAsync, when to choose one over the other?

runAsync takes Runnable as input parameter and returns CompletableFuture<Void>, which means it does not return any result.

CompletableFuture<Void> run = CompletableFuture.runAsync(()-> System.out.println("hello"));

  But suppyAsync takes Supplier as argument and returns the CompletableFuture<U> with result value, which means it does not take any input parameters but it returns result as output.

CompletableFuture<String> supply = CompletableFuture.supplyAsync(() -> {
        System.out.println("Hello");
        return "result";
    });

 System.out.println(supply.get());  //result
Conclusion : So if you want the result to be returned, then choose supplyAsync or if you just want to run an async action, then choose runAsync.
  
### Exception Handling of CompletableFuture
by using the following methods  
public CompletableFuture <T> exceptionally(Function <Throwable, ? extends T> function);  
public <U> CompletableFuture<U> hadle(BiFunction<? super T, Throwable, ? extends U> bifunction);  
public CompletableFuture<T> whenComplete(BiConsumer<? super T, ? super Throwable> action);  

what is fork join
The fork-join framework allows to break a certain task on several workers and then wait for the result to combine them. It leverages multi-processor machine's capacity to great extent. Following are the core concepts and objects used in fork-join framework.
~~~

public class TestThread {

   public static void main(final String[] arguments) throws InterruptedException, 
      ExecutionException {
      
      int nThreads = Runtime.getRuntime().availableProcessors();
      System.out.println(nThreads);
      
      int[] numbers = new int[1000]; 

      for(int i = 0; i < numbers.length; i++) {
         numbers[i] = i;
      }

      ForkJoinPool forkJoinPool = new ForkJoinPool(nThreads);
      Long result = forkJoinPool.invoke(new Sum(numbers,0,numbers.length));
      System.out.println(result);
   }  

   static class Sum extends RecursiveTask<Long> {
      int low;
      int high;
      int[] array;

      Sum(int[] array, int low, int high) {
         this.array = array;
         this.low   = low;
         this.high  = high;
      }

      protected Long compute() {
         
         if(high - low <= 10) {
            long sum = 0;
            
            for(int i = low; i < high; ++i) 
               sum += array[i];
               return sum;
         } else {	    	
            int mid = low + (high - low) / 2;
            Sum left  = new Sum(array, low, mid);
            Sum right = new Sum(array, mid, high);
            left.fork();
            long rightResult = right.compute();
            long leftResult  = left.join();
            return leftResult + rightResult;
         }
      }
   }
}
~~~
