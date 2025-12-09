Camel-casing:
- Export use UPPER case
- Non exported use LOWER case

Style:
Lines of code should be packed together within function body

Defer delays the execution of the contained code until the surrounding function returns

Method vs Receiver:
- A method contains a receiver whereas a function does not
- Methods of the same name but different types can be defined in the program whereas functions cannot
- A method cannot be used as a first-order object whereas a function can (can be constructed at runtime, passed as a parameter, returned from a function, or assigned to a variable)

Mutex hats
Just a visual queue for programmers which should be used for multithreading
Lock placed on top of data it protects

Polymorphism:
	Contracts - Interfaces are implemented implicitly
	Embedding - prefer composition over inheritance
	- Has a vs is a
	- Duck typing
	- embedding interfaces in iinterfaces
	- Embedding types in structs
	- Implementing interfaces provides polymorphism
	Generality - When only the interface behaviour matters do not export value type itself
	Interfaces effectively do dynamic dispatch
	- Run time instead of compile time

Panic/recover
- Exceptions are not a feature of go
- Panic used for unrecoverable errors, for halting an entire server request, to propagate errors up the stack within a package
- Used very rarely

Dave Cheney is a go advocate that gives best practice examples

In go the unit of encapsulation is the package (see capitalization above)

CSP (Communicating Sequential Processes) is a formal language for describing patterns of interaction in concurrent systems
	Tool for specifying and verifying the concurrent aspects of a system
	Uses include to find deadlock and livelock scenarios

Go implements the channel and message passing aspects of CSP via channels
Go implements to process aspects of CSP via goroutines

Amdahls law defines the upper bound of program speed up via parallelism
Parallel programs are more difficult to write due to race conditions and the need for communication and syncronization
Types of parallelism are bit, instruction, data, and task
Parallel computers can be multicore or clusters (multiple machines working on a task)

Concurrency is the decomposability a program into order-independent or partially-ordered components
- It is possible to have parallelism without concurrency and concurrency without parallelism
- Concurrency does not mean parallel

Mutex is taken and released, semaphore is meant to signal or wait

Subroutines are a sequence of program instructions that performs a specific task
Coroutines are computer program components that generalize subroutines for non-preemptive multitasking by allowing execution to be suspended and resumed
- Concurrent but not parallel
Goroutines are concurrent and parallel
- Lightweight and much cheaper than threads
- Return immediately so non-blocking
- Capable or running concurrently with other functions
When a go/coroutine blocks the run-time automatically moves an available coroutine onto the underlying OS thread
Today the go runtime can switch goroutines when
- A goroutine exits
- a goroutine makes a blocking system call
- A goroutine makes a blocking runtime call
- Occasionally when calling a normal go function

Channels are a typed conduit through which you can send and receive values with the channel operator: <-
- Channels are allocated via a call to make() : c:=make(chan int)
- Channels are the main method of communication between goroutines
- Block until both sides are ready
- Can be unbuffered or buffered

- Unbuffered combine exchange of data with synchronization
- Buffered can transfer data asynchronously

The sync package provides a safe mechanism for initialization in presences of multiple goroutines
- Also provides mutex (all locks are exclusive) and RWMutex (W locks are exclusive and R locks can be shared)
- Conditions are a rendezvous point for go routines waiting for or announcing the occurrence of an event
	- Broadcast wakes all goroutines waiting on c
	- Signal wakes one goroutine waiting on c
	- Wait atomically unlocks c.L and suspends execution of the calling goroutine and cannot return unless awoken by broadcast or signal
- Pools are a set of temporary objects that may be individually saved and retrieved
- The purpose of a pool is to cache allocated but unused items for later reuse, relieving pressure on the garbage collector
- Used to manage a group of temporary items silently shared among and potentially reused by concurrent Independent clients of a package
- WaitGroup is a type used to wait for a collection of goroutines to finish. The main goroutine calls add to set the number of goroutines to wait for
	- Each of the goroutines runs and calls done when finished
	- Add, done, wait are the functions of waitgroup. Increment, decrement, and block until waitgroup counter is zero respectively
	- If counter becomes negative a panic occurs
- Structural embedding is when you embed a mutex within a struct
	- Embedded types create anonymous fields accessed through the instance itself
- Sync.map is used only for write once read many on a key
	- Multiple go routines doing Create, read, update, delete (CRUD) against disjoint keys
	- Generally not preferred over a normal go map

Channels
- Channels provide a way for two goroutines to communicate with each other and synchronize their execution
- Channels are thread safe
- Many goroutines can share a single channel
- Can specify channel direction which is checked at compile time
- Go has a special statement called select which allows a task to wait on multiple channels
- Waitgroups and select statements are the most complex part of go so focus on learning
- Normally channels are synchronous but a buffered channel allows send and receive operations to be performed asynchronously without blocking until the channel buffer is full
	- Add int to the arguments in the channel make command
- The ordering and scheduling of goroutines outside of the synchronization provided by channels is nondeterministic
- If a goroutine ever chooses to read write to a channel at the same time that all other goroutines are waiting on channels the program can no longer progress
- Closing a channel indicates that no more values will be sent on it
	- Reading from a closed channel produces the channels "Zero" value and a false "more" flag
	- Writing to a closed channel causes a panic
	- Channels are first class citizens so they can be passed to functions returned from functions, used as receivers in method definitions

Context
- Go provides a standard library package to simplify and standardize context propagation and control
- Implements support for execution deadlines and cancellation
- The context interface contains Done(), Err(), Deadline(), Value()
- Best Practice:
	- Pass context parameter called ctx as first argument
	- Use context values only for request scoped data that transits processes and APIs
	- Do not pass a nil context
	- The same context may be passed to many goroutines, don’t create multiple contexts unnecessarily
	- Pass context to every function on the call path between incoming and outgoing requests
	- Do not store contexts inside a struct type
	- Server frameworks that want to build on context should provide implementation of context to bridge between custom package features and those that expect a standard go contect parameter

Unit testing and mocking
- mocks are generated for interfaces