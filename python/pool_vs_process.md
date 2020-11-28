# Pool과 Process의 차이


‘Process’ halts the process which is currently under execution and at the same time schedules another process.   
‘Pool’ on the other hand waits till the current execution in complete and doesn’t schedule another process until the former is complete which in turn takes up more time for execution.

‘Process’ allocates all the tasks in the memory whereas ‘Pool’ allocates the memory to only for the executing process.   
You would rather end up using Pool when there are relatively less number of tasks to be executed in parallel and each task has to be executed only once.




### Below information might help you understanding the difference between Pool and Process in Python multiprocessing class:

Pool:    
When you have junk of data, you can use Pool class.  
Only the process under execution are kept in the memory.  
I/O operation: It waits till the I/O operation is completed & does not schedule another process. This might increase the execution time.  
Uses FIFO scheduler.  


Process:    
When you have a small data or functions and less repetitive tasks to do.  
It puts all the process in the memory. Hence in the larger task, it might cause to loss of memory.  
I/O operation: The process class suspends the process executing I/O operations and schedule another process parallel.  
Uses FIFO scheduler.


**Pool**  
Pool은 주어진 processor 갯수로 작업을 순서에 상관없이 할당하여 순서가 뭉개진다.  
또한 할당된 작업이 끝나야 다른 작업을 메모리 올려서 수행한다.  
일반적으로 작업의 수가 processor 개수보다 클때 사용한다.  

**Process**  
반면 Process는 메모리에 전부 올려놓고 cpu core processor를 가능한 많이 사용하여 작업을 한다.  
따라서 순서 유지가 가능하지만, 메모리가 Pool 보다는 더 많이 잡아 먹게 된다.  
일반적으로 작업의 수가 작고 해당 task를 한번만 해도 되면 process를 사용한다.  



## map_async
map_async의 경우 map이 비동기로 돌아간다.  
일반 map의 경우 map이 다 끝나야 다른 작업 (다른 라인)으로 넘어가는데, map_async의 경우 백그라운드에서 작업되어 바로 다른 작업 (다른 라인)으로 넘어간다.  
pool.map_async(f, ...).wait() 을 사용하면 map 처럼 사용이 가능하다

https://stackoverflow.com/questions/35908987/multiprocessing-map-vs-map-async

### Reference

https://lih-verma.medium.com/multi-processing-in-python-process-vs-pool-5caf0f67eb2b  
https://www.ellicium.com/python-multiprocessing-pool-process/  
