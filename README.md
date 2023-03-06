# readers-writers
In the solution which is discussed in the class, readers are having more priority and if one reader process is invoked while the other is being executed, the current reader process is also added to the reading queue and this process of reading continues till the number of reading processes which are waiting are zero. And the writing processes which are in the queue go unnoticed. 
# readers
In this new solution, we will ensure that the reading and writing processes are being executed in the order they arrive. We ensure this by letting the writer's process begin only when the count of reading processes going on is zero. For this, we maintain a semaphore named as readcn. Multiple reading processes can be performed simaltaneously using this algorithm.
# writers
   If a writing process is in it's queue waiting for the readcn to become zero, the other reading process which arrives is not going to start because we initiate the reading process by ensuring that no writing process is waiting in the writing queue. We achieve this by maintaining a semaphore named wfwc(wait for writing count).
# Example
       Now we consider an example and ensure the correct working of this algorithm. W1 W2 R1 R2 W3
       Initially the readcn and wfwc are both initialized to zero.
       Since the readcn is zero initially, both the writer's process increment the wfwc and perform the writing processes one after the other by using wrt semaphore. In this time, R1 and R2 which are arrived will not be started because first step in their execution is checking whether wfwc ==0. Once W1 and W2 complete their execution and wfwc is made zero and the reading processes R1 and R2 are initiated. 
       R1 and R2 increment the readcn ad perform the reading process simaltaneously(if needed) and after that decrement the readcn.
    W3 process which is waiting is not initiated while R1 and R2 are being executed as readcn!=0. After R1 and R2 completion, W3 will be initiated by incrementing wfwc. And the writing process is carried out without any other process using the shared memory simaltaneously.
