# Concurrency Control

* **A Concurrency Control** protocol is the method that the dbms uses to ensure correct results 
  for concurrent operations on a shared object
  
* A protocol correctness criteria can vary:
    * **Logical Correctness**: Can I see the data that I am supposed to see
    * **Physical Correctness**: is the internal representation of the object sound

# Locks vs Latches

## Locks

* protect the database's logical content from other transactions
* Held for the transaction duration
* Need to be able to rollback changes

## Latches

* protect the critical sections of the DBMS internal data structure from other <u>threads</u>
* Held for operation duration
* Do not need to be able to rollback changes


# Latches

## Latch Modes

### Read Mode

* Multible threads can read the same object at the same time
* A thread can acquire the read latch if another thread has it in read mode

### Write Mode

* Only one thread can access the object
* A thread cannot acquire a write latch if there is another thread has it in any mode


## Latch Implementation

* Approach #1: Blocking OS mutex:
    * simple to use
    * non-scalable
    * example: std::mutex
* Approach #2: Test-and-Set spin latch:
    * very effecient(1 instruction to latch or unlatch)
    * non-scalable, not cache friendly
    * example: std::atomic<T>
    ```
    std::atomic_flag latch;
    while(latch.test_and_set(...)){
        //retry? yield? abort?
    }
    ```
* Approach #3: Reader-Writer Latch:
    * Allows for concurrent Read
    * Must manage read/write queues to avoid starvation
    * can be implemented on the top of spinlock 

## Hash Table Latching 
* All threads moves in the same direction and only access a single page/slot at a time (in case of linear proping)
* deadlock are not possible 

* to resize a table, take a latch on the entire table 


* Approach #1: Page Latches:
    * each page has its own reader-writer latch that protects the entire content
    * threads acquire either a reader or writer latch before accessing the pagem
* Approach #2: Slot latches:
    * each slot has its own latches
    * Can use a single mode latch to reduce meta-data and computational overhead    

## B+tree Concurrency Control

