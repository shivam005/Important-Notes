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

6). invokeAll(Callable<T> task) -> It is the blocking function which executes the list of tasks and waits for all of them to finish and returns the list of future as the same order tasks provided to method. 

7). invokeAny(Callable<T> task) -> It waits for atleast one task to get completed and returns the result (not the future) for a completed task and cancels any unfinished tasks. 

##### Future
1). boolean isDone() -> It returns the boolean value and checks whether the task has completed or not. Completion means termination, exception or cancellation. 

2). boolean isCancelled() -> returns true if this task was cancelled befire it completed normally. 

3). boolean cancel(boolean mayinterruptIfRunning) -> Attempts to cancel a task, returns true if cancelled suceesfully and false it already completed or could not cancel. 

4). V get() -> wait if necessary for the computation to complete and then retrieves the result. 

5). V get(long timeout, TimeUnit unit) -> wait for the given time and then retrieves the result if any or gives timeout. 

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

```
```
#### newFixedThreadPool(nThreads)
Uses a fixed number of threads operating off a shared unbounded queue. If all threads are active, new tasks wait in the queue.
#### newCachedThreadPool()
Creates new threads as needed but will reuse previously constructed threads when they are available. Threads that are idle for 60 seconds are terminated and removed from the cache.
#### newSingleThreadScheduledExecutor()
To run tasks after certain delay or to run task periodically. 
#### newScheduledThreadPool(corePoolSize)
Same as scheduled thread pool, just it takes corepoolsize as input. 
#### newWorkStealingPool()
Suitable for a large number of short-lived tasks that can be efficiently distributed among available processors.
