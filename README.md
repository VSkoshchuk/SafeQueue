# SafeQueue
SafeQueue is an implementation of the thread/IRQ safe queue that does not use dynamic memory, and can perform sumultaneously pop() and push() without any blocking, that alows use this implementation as data container in the critical sections or threads and IRQ where it is impossible to wait for access to the container and data loss is unacceptable.
