Master-Worker Synchronization with Read-Write Lock
Overview
This project demonstrates a synchronization mechanism between producer (master) and consumer (worker) threads using mutexes and condition variables in C. It also includes an implementation of a read-write lock. The program ensures correct synchronization and efficient handling of multiple producer and consumer threads operating on a shared buffer.

Features
Producer-Consumer Synchronization: Utilizes mutexes and condition variables to synchronize access to a shared buffer.
Read-Write Lock Implementation: Provides a custom read-write lock to manage concurrent read and write access to shared data.
Requirements
GCC (or any other C compiler)
POSIX Threads (pthread) library
Files
main.c: Contains the main program logic for the producer-consumer synchronization.
rwlock.h: Header file for the read-write lock implementation.
rwlock.c: Source file for the read-write lock functions.
Compilation and Execution
Compilation
To compile the program, run:

sh
Copy code
gcc -o master-worker main.c rwlock.c -lpthread
Execution
To execute the program, run:

sh
Copy code
./master-worker <total_items> <max_buf_size> <num_workers> <num_masters>
For example:

sh
Copy code
./master-worker 10000 1000 4 3
This command initializes the program to produce 10,000 items with a buffer size of 1,000, 4 worker threads, and 3 master threads.

Usage
Functions
Producer (Master) Threads:

generate_requests_loop(void *data): Produces items and places them in the buffer. Ensures synchronization using mutexes and condition variables.
Consumer (Worker) Threads:

consume_requests_loop(void *data): Consumes items from the buffer. Ensures synchronization using mutexes and condition variables.
Read-Write Lock:

InitalizeReadWriteLock(struct read_write_lock *rw): Initializes the read-write lock.
ReaderLock(struct read_write_lock *rw): Acquires the read lock.
ReaderUnlock(struct read_write_lock *rw): Releases the read lock.
WriterLock(struct read_write_lock *rw): Acquires the write lock.
WriterUnlock(struct read_write_lock *rw): Releases the write lock.
Detailed Flow
Initialization:

The program initializes the buffer and thread-related variables based on user input.
Creates and starts the specified number of master and worker threads.
Synchronization:

Masters produce items and place them in the buffer while ensuring the buffer does not overflow.
Workers consume items from the buffer while ensuring the buffer does not underflow.
Termination:

The program waits for all master threads to finish producing items.
After all master threads have finished, it signals worker threads to finish consuming remaining items in the buffer.
Finally, the program joins all threads and deallocates resources.
Example Output
The output consists of messages indicating the production and consumption of items by the master and worker threads:

csharp
Copy code
Produced 0 by master 0
Produced 1 by master 1
Consumed 0 by worker 0
Consumed 1 by worker 1
...
master 0 joined
master 1 joined
worker 0 joined
worker 1 joined
...
