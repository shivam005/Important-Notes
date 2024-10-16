### ExecutorService:: To run task asynchronously
#### newSingleThreadExecutor()
Uses a single worker thread and used when no two task needs to be executed concurrently. 
```
public class Concurrency {

    public static void main(String[] args) {
        System.out.println(Thread.currentThread().getName() + " is running in first line");
        ExecutorService executorService = Executors.newSingleThreadExecutor();
        executorService.execute(() -> {
            for (int i = 0; i < 4; i++) {
                System.out.println(Thread.currentThread().getName() + " is running with first task");
            }
        });
        executorService.execute(() -> {
            for (int i = 0; i < 4; i++) {
                System.out.println(Thread.currentThread().getName() + " is running with second task");
            }
        });
        System.out.println(Thread.currentThread().getName() + " is running in last line");
        executorService.shutdown();
    }
}
Output:
main is running in first line
pool-1-thread-1 is running with first task
pool-1-thread-1 is running with first task
pool-1-thread-1 is running with first task
pool-1-thread-1 is running with first task
pool-1-thread-1 is running with second task
pool-1-thread-1 is running with second task
pool-1-thread-1 is running with second task
pool-1-thread-1 is running with second task
main is running in last line
```
1). execute(Runnable task) -> This takes runnable as the input and does not return anything. (Fire and Forget)

2). shutdown() -> It is necessary to shutdown the executor in the finally block or else It will keep on waiting for the other task to be assigned and would waste resource. 
This method waits for all the task to be completed and then shuts down the executor. 

3). shutdownNow() -> It will abruptly stop the executor so It will also stop all the task which is being processed and in return, it would give the list of (runnable) unfinished tasks.

4). submit(Runnable task) -> This takes runnable as the input and return future which consist of info related to task rather than actual output.

5). submit(Callable<T> task) -> This takes callable as the input and return the future as the output of pending task result.
```
public class Concurrency {

    public static void main(String[] args) throws ExecutionException, InterruptedException {
        System.out.println(Thread.currentThread().getName() + " is running in first line");
        ExecutorService executorService = Executors.newSingleThreadExecutor();
        Future<Integer> result1 = executorService.submit(() -> 2 + 3);
        System.out.println("result from " + Thread.currentThread().getName() + " is " + result1.get());
        Future<Integer> result2 = executorService.submit(() -> 5 + 6);
        System.out.println("result from " + Thread.currentThread().getName() + " is " + result2.get());
        System.out.println(Thread.currentThread().getName() + " is running in last line");
        executorService.shutdown();
    }
}
Output:
main is running in first line
result from main is 5
result from main is 11
main is running in last line
```

6). invokeAll(Callable<T> task) -> It is the blocking function which executes the list of tasks and waits for all of them to finish and returns the list of future as the same order tasks provided to method. 
```
public class Concurrency {

    public static void main(String[] args) throws ExecutionException, InterruptedException {
        System.out.println(Thread.currentThread().getName() + " is running in first line");
        ExecutorService executorService = Executors.newSingleThreadExecutor();
        Callable<Integer> task1 = () -> 2 + 3;
        Callable<Integer> task2 = () -> 5 + 3;
        List<Future<Integer>> futures = executorService.invokeAll(Arrays.asList(task1, task2));
        for(int i=0; i<futures.size();i++){
            System.out.println("Outputs are "+ futures.get(i).get());
        }
        System.out.println(Thread.currentThread().getName() + " is running in last line");
        executorService.shutdown();
    }
}
Output:
main is running in first line
Outputs are 5
Outputs are 8
main is running in last line
```

7). invokeAny(Callable<T> task) -> It waits for atleast one task to get completed and returns the result (not the future) for a completed task and cancels any unfinished tasks. 

##### Future
1). boolean isDone() -> It returns the boolean value and checks whether the task has completed or not. Completion means termination, exception or cancellation. 

2). boolean isCancelled() -> returns true if this task was cancelled befire it completed normally. 

3). boolean cancel(boolean mayinterruptIfRunning) -> Attempts to cancel a task, returns true if cancelled suceesfully and false it already completed or could not cancel. 

4). V get() -> wait if necessary for the computation to complete and then retrieves the result. 

5). V get(long timeout, TimeUnit unit) -> wait for the given time and then retrieves the result if any or gives timeout. 


 
#### newFixedThreadPool(nThreads)
Uses a fixed number of threads operating off a shared unbounded queue. If all threads are active, new tasks wait in the queue.
#### newCachedThreadPool()
Creates new threads as needed but will reuse previously constructed threads when they are available. Threads that are idle for 60 seconds are terminated and removed from the cache. dynamically grow and shrink as needed.
#### newSingleThreadScheduledExecutor()
To run tasks after certain delay or to run task periodically. It extends executor service hence It has all the methods in common and additionally It has following methods:
1). public <V> ScheduledFuture<V> schedule(Callable<V> callable, long delay, TimeUnit unit);

2). public ScheduledFuture<?> scheduleAtFixedRate(Runnable command, long initialDelay, long period, TimeUnit unit);

3). public ScheduledFuture<?> scheduleWithFixedDelay(Runnable command, long initialDelay,long delay,TimeUnit unit);
```
public class Concurrency {

    public static void main(String[] args) throws ExecutionException, InterruptedException {
        System.out.println(Thread.currentThread().getName() + " is running in first line");
        ScheduledExecutorService executorService = Executors.newSingleThreadScheduledExecutor();
        Runnable task1 = () -> System.out.println("Hi There, Task 1");
        Callable<String> task2 = () -> "Hi There, Task 2";
        ScheduledFuture<?> scheduledFuture = executorService.scheduleWithFixedDelay(task1, 5, 5, TimeUnit.SECONDS);
        System.out.println(scheduledFuture.get());
        System.out.println(Thread.currentThread().getName() + " is running in last line");
        executorService.shutdown();
    }
}
Output:
main is running in first line
Hi There, Task 1
Hi There, Task 1
Hi There, Task 1
Hi There, Task 1
.
.
.
Hi There, Task 1
```

#### newScheduledThreadPool(corePoolSize)
Same as scheduled thread pool, just it takes corepoolsize as input. 
#### newWorkStealingPool()
Suitable for a large number of short-lived tasks that can be efficiently distributed among available processors.

#### Use two thread to count the number of elements in the array
```
 public AtomicInteger print(int[]  arr){
        ExecutorService executorService = null;
        AtomicInteger atomicInteger = new AtomicInteger();
        try {
            executorService = Executors.newFixedThreadPool(5);
            executorService.submit(() -> {
                for (int i = 0; i < arr.length / 2; i++) {
                    atomicInteger.incrementAndGet();
                }
            });
            executorService.submit(() -> {
                for (int i = arr.length / 2; i < arr.length; i++) {
                    atomicInteger.incrementAndGet();
                }
            });
            return atomicInteger;
        }catch (Exception e){

        }finally {
            executorService.shutdown();
        }
        return atomicInteger;
    }
```
#### Print n number using two threads
```
    public AtomicInteger print(int n){
        ExecutorService executorService = null;
        AtomicInteger atomicInteger = new AtomicInteger();
        try {
            executorService = Executors.newFixedThreadPool(5);
            executorService.submit(() -> {
                    for(int i=0; i<n/2;i++){
                        int i1 = atomicInteger.incrementAndGet();
                        System.out.println(Thread.currentThread()+":"+i1);
                    }
            });
            executorService.submit(() -> {
                for(int i=n/2; i<n;i++){
                    int i1 = atomicInteger.incrementAndGet();
                    System.out.println(Thread.currentThread()+":"+i1);
                }
            });
            return atomicInteger;
        }catch (Exception e){

        }finally {
            executorService.shutdown();
        }
        return atomicInteger;
    }
// Output: Will not be in order.
```
#### Print n number using two threads, in ordered fashion
Here, I am using the countdownlatch to achieve this. I am using two methods of countdownlatch which is countDown() and await(). So, when we will invoke the countdown method then it would say that the first thread has finished its task and the other thread can execute and the other method which await wouild be called on the second one which would wait for the countdown() to be invoked. 
(It is useless as we are making other one to wait then why not to write the single threaded code or go for better option.) 
```
  public AtomicInteger print(int n){
        CountDownLatch latch = new CountDownLatch(1);

        ExecutorService executorService = null;
        AtomicInteger atomicInteger = new AtomicInteger();

        try {
            executorService = Executors.newFixedThreadPool(5);
            executorService.submit(() -> {
                    for(int i=0; i<n/2;i++){
                        int i1 = atomicInteger.incrementAndGet();
                        System.out.println(Thread.currentThread()+":"+i1);
                    }
                    latch.countDown();
            });
            executorService.submit(() -> {
                for(int i=n/2; i<n;i++){
                    try {
                        latch.await();
                    } catch (InterruptedException e) {
                        throw new RuntimeException(e);
                    }
                    int i1 = atomicInteger.incrementAndGet();
                    System.out.println(Thread.currentThread()+":"+i1);
                }
            });
            return atomicInteger;
        }catch (Exception e){

        }finally {
            executorService.shutdown();
            try {
                executorService.awaitTermination(5, TimeUnit.NANOSECONDS);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        return atomicInteger;
    }

```
#### What will happen when two different synchronized method inside a class are being invoked by two different thread
Since they both are associated with one object, hence when the first thread would be executing first method then second thread will have to wait to invoke the second method as the intrinsic lock will get applied on an object. 
Hence, the solution to this problem is to avoid the method level synchornization and to put the lock over the lines of code which is there in critical section. 

#### Fork-Join Pool
Herein, whenever we fork any constructor it internally invokes the compute method and recursively It goes on reduced upto the threshold and then the actual method get invoked. Finally It computes the result and returns it and then finally using join() we merge them and return them.
1. <T> ForkJoinTask<T> submit(Callable<T> task) :: Submits a Callable task for execution and returns a ForkJoinTask representing the task.
2. ForkJoinTask<?> submit(Runnable task) :: Submits a Runnable task for execution and returns a ForkJoinTask representing the task.
3. <T> T invoke(ForkJoinTask<T> task) :: Submits a ForkJoinTask for execution and waits for its completion, then returns the result.
4. void execute(Runnable task) :: Executes a Runnable task asynchronously
```
 package org.java.practicepackage;

import java.util.concurrent.*;

public class ForkJoinSearch extends RecursiveTask<Integer> {

    Integer target;
    int[] arr;
    int left;
    int right;

    public  ForkJoinSearch(Integer target, int[] arr,  int left, int right){
        this.target = target;
        this.arr= arr;
        this.left=left;
        this.right = right;
    }

    @Override
    protected Integer compute() {
        int size = left - right + 1;
        if(size>3){
        int mid = (left+right)/2;
        ForkJoinSearch task1= new ForkJoinSearch(   target, arr, 0,mid );
        ForkJoinSearch task2= new ForkJoinSearch(      target, arr, mid, arr.length -1);
        task2.fork();
        task1.fork();
        int result = task1.join() + task2.join();

        return result;}
        else {
            return find();
        }
    }

    public Integer find(){
        int count=0;
        for(int i=0; i< arr.length;i++){
            if(arr[i]==target){
                count++;
            }
        }
        return count;
    }
    public static void main(String[] args) throws ExecutionException, InterruptedException {
        long l = System.currentTimeMillis();
        int[] arr = {2,2,2,2,2,3,2,2,5,5,1,5,2,2,2,2,3,2,2,5,5,1,5,2,2,2,2,3,2,2,5,5,1,5,2,2,2,2,3,2,2,5,5,1,5};
        int target =2;
        ForkJoinSearch task= new ForkJoinSearch( 2, arr, 0, arr.length-1);
        ForkJoinPool pool = new ForkJoinPool();
        Integer invoke = pool.invoke(task);
        System.out.println(invoke);
        long k = System.currentTimeMillis();
        System.out.println( k-l +" "+ TimeUnit.MILLISECONDS);
    }
}

```
### Semaphore
A semaphore is used to manage the number of concurrent accesses that can be granted to threads. We can set the number of permits in the semaphore, and based on the number of permits, threads will be able to access a resource concurrently.




