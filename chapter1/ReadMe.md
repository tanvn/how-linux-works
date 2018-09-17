#### Levels and layers of abstraction in a Linux System
_kernel_ is software residing in memory telling CPU what to do.

_processes_ are the running programs that the kernel manages, run in _user process_.

_kernel_ runs in _kernel mode_  and the user processes run in _user mode_.

The act of one process giving up control of the CPU to another process is called a _context switch_.

A _time slice_ gives a process enough time for significant computation and it's too small that humans can't perceive the interruption.
The kernel is responsible for context switching.

1. The CPU (the actual hardware) interrupts the current process based on an internal timer, switches into kernel mode, and hands control back to the kernel.

2. The kernel records the current state of the CPU and memory, which will be essential to resuming the process that was just interrupted.

3. The kernel performs any tasks that might have come up during the preceding time slice (such as collecting data from input and output, or I/O, operations).

4. The kernel is now ready to let another process run. The kernel analyzes the list of processes that are ready to run and chooses one.

5. The kernel prepares the memory for this new process, and then prepares the CPU.

6. The kernel tells the CPU how long the time slice for the new process will last.

7. The kernel switches the CPU into user mode and hands control of the CPU to the process.

#### The kernel

The kernel is in charge of managing tasks in 4 general system areas :
- Processes
- Memory
- Device drivers
- System calls and support

#### System calls and support
- **fork()** When a process calls fork(), the kernel creates a nearly identical copy of the process.
- **exec()** When a process calls exec(program), the kernel starts program, replacing the current process.

#### User

Root is known as _superuser_

As powerful as the root user is, it still runs in the operating system's user mode, not kernel mode.

_groups_ are sets of users, it allows a user to easily share file access to other users in the same group. 