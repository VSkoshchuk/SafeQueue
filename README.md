SafeQueue
==========================

## Summary
SafeQueue is an implementation of the thread/IRQ safe queue that does not use dynamic memory and can perform simultaneously pop() and push() without any blocking, which allows the use of this implementation as a data container in critical sections, or threads and IRQ where it is impossible to wait for access to the container and data loss is unacceptable. Developed with a focus on embedded systems.

The problem being addressed involves needing a special kind of container that allows different streams or Interrupt Service Routines (ISRs) to add and remove elements independently. This container is designed to prevent issues that arise when the same threads simultaneously call the 'push' and 'pop' methods. It also enables different threads to call these methods at the same time without causing any internal delays. This means that if an operation like removing an element is interrupted, the container can still handle adding new elements smoothly, and vice versa.

To illustrate, imagine a situation where an interrupt requires adding an element to a queue, while at the same time, a main loop is removing elements from this queue. In such cases, standard containers would need synchronized access in the main loop to avoid altering the internal state during an interruption. However, this approach has a downside: if an interrupt happens while the main loop is active, it will be unable to access the container until the main loop finishes and releases the mutex (a mechanism to ensure mutual exclusion). This delay can result in the loss of data. The proposed container aims to solve this issue by allowing uninterrupted access during such concurrent operations.

## Usage
Here's a simple and clear example of using SafeQueue without threading, illustrating how to push and pop elements, as well as access the front and back elements of the queue.
```c++
int main() {
    // Create a SafeQueue with a capacity for 5 integers
    SafeQueue<int, 5> queue;
    int value = 10;
    int values[4] = {20, 30, 40, 50};

    // Pushing elements into the queue
    queue.push(&value);
    queue.push(values, 4);

    // Displaying the front and back elements
    std::cout << Size: " << queue.size() << std::endl; // Should be 5
    std::cout << "Front element: " << *queue.front() << std::endl; // Should be 10
    std::cout << "Back element: " << *queue.back() << std::endl;  // Should be 50

    // Popping an element from the queue
    queue.pop();
    queue.pop(2)

    // Displaying the front element after popping
    std::cout << Size: " << queue.size() << std::endl; // Should be 2
    std::cout << "New front element: " << queue.front() << std::endl; // Should be 40

    return 0;
}
```

## Authors
1. VSkoshchuk (<skoschuk999@gmail.com>)
