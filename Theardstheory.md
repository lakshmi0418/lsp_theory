### why we are using pthread_create instead of clone() for creating threads?
We use pthread_create() instead of clone() for creating threads in user applications mainly because of portability, ease of use, and safety. 
| Feature                   | `pthread_create()`        | `clone()`                      |
| ------------------------- | ------------------------- | ------------------------------ |
| Portability               | ✅ POSIX-standard          | ❌ Linux-only                   |
| Ease of Use               | ✅ High-level API          | ❌ Low-level, complex           |
| Resource Management       | ✅ Handled by library      | ❌ Manual                       |
| Integration with pthreads | ✅ Seamless                | ❌ Not integrated               |
| Use Case                  | App-level thread creation | Kernel-level or advanced cases |

### why a stack grows?
A stack grows because it needs to store more data, especially as a program runs and makes function calls.

The stack grows because each function call needs memory for its execution context (local variables, return addresses, etc.). This is a normal and essential behavior for structured execution flow in programming. However, excessive or uncontrolled growth (e.g. deep recursion) can lead to stack overflows, so it's important to design with stack limits in m
### what segments are shared by multiple threads within a process?
n a multithreaded process:

    Shared segments include: code (text), data, heap, open files, and memory mappings.

    Private segments include: each thread’s stack, CPU registers, and thread-local storage.

This design allows threads to communicate efficiently via shared memory but also requires careful synchronization (mutexes, semaphores) to avoid data races.

### can you fetch the thread entry point return value in your main thread?
Yes, you can fetch a thread's entry point return value in your main thread — using pthread_join() in POSIX threads.
yes, you can fetch a thread’s return value in the main thread using pthread_join(). This is a common and clean way to collect results from worker threads in C/C++ with pthreads.
### Explain the working of pthread_mutex_trylock()?
pthread_mutex_trylock() is a non-blocking version of pthread_mutex_lock() used to attempt to lock a mutex. It’s useful when you want to try acquiring a lock without waiting, allowing your thread to do something else if the lock isn't availab
How It Works

    If the mutex is currently unlocked, pthread_mutex_trylock():

        Locks the mutex

        Returns 0 (success)

    If the mutex is already locked by another thread, it:

        Does NOT block

        Returns EBUSY immediately (indicating the mutex is already in use)

    If the mutex is invalid or uninitialized:

        Returns an appropriate error code, like EINVAL.


### Explain the application of pthread_mutex_timelock()?
thread_mutex_timedlock() lets a thread wait for a mutex with a timeout, giving you finer control over thread synchronization. It’s especially valuable when you can’t afford to wait forever to acquire a lock — making it ideal for real-time, responsive, or robust multi-threaded applications.
### what is mutual exclusion?
Mutual exclusion (mutex) is a fundamental concept in concurrent programming that ensures that only one thread (or process) at a time can access a shared resource or critical section.

### Advantage of Thread over process?
hreads are preferred over processes when:

    You need high performance

    You need to handle many tasks concurrently

    You want to share data easily between tasks

They are lighter, faster, and more communication-friendly than processes — making them ideal for modern, high-concurrency applications.
### Advantage of process over Thread?
Processes offer:

    Better isolation

    Crash containment

    Security

    Stability

They are ideal when:

    You need robust error handling

    You're running untrusted code
    So while threads are fast and lightweight, processes are safe and stable — and each is better suited for different types of applications.
### How do you overcome this updation or synchronization issue.when the multiple threads are tryingto access the global variables?
When multiple threads access or update global variables, it can lead to race conditions, data corruption, or unexpected behavior. To overcome this synchronization issue, you need to protect shared resources using proper thread synchronization mechanisms.
pthread_mutex_t lock = PTHREAD_MUTEX_INITIALIZER;
int global_counter = 0;

void* increment(void* arg) {
    pthread_mutex_lock(&lock);
    global_counter++; // Critical section
    pthread_mutex_unlock(&lock);
    return NULL;
}
### How much cpu time is given to user space thread and kernel space thread?
### Explain POSIX and system-v difference?
### what are the points to remember when mutex locks are used to protect the critical section?
### By using mutex_lock what you are acheiving?
### Difference between mutex locks and semaphore?
### Explain the variants of pthread_mutex_lock?
### How to create a thread?
### Explain the compilation of a thread?
### what are the arguments of pthread_create?
### Explain the return value of thread?

