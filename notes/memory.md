[CS 1C - Lec_2a](../CS%201C%20-%20Lec_2a.docx)


[CS 1C - Lec_2b-Runtime stack - DIAGRAM](../CS%201C%20-%20Lec_2b-Runtime%20stack%20-%20DIAGRAM.docx)

Note: The spaces in filenames are URL-encoded as %20 to ensure they are correctly linked.


Of course! Here's the information reformatted in GitHub markdown:

---

### **Runtime Stack (Call Stack)**

1. **Overview**
   - The Runtime Stack (or Call Stack) is a specialized data structure that tracks function calls in a program. When a function is called, its details are added to the stack, and when it finishes, its details are removed. This structure ensures that functions can call other functions and return correctly.

2. **Stack Segment (`ss`)**
   - Each process's memory layout contains a section named the stack segment. This segment hosts the call stack.

3. **Memory Location**
   - The call stack resides towards the higher addresses in memory.

4. **Stack Pointer (`ESP`)**
   - The `ESP` (Extended Stack Pointer) is a CPU register that points to the top of the stack. It adjusts as items are pushed onto or popped off the stack.

5. **Operations: Push and Pop**
   - **Push**: Add an item to the top of the stack.
   - **Pop**: Remove the topmost item from the stack.
   - The `ESP` adjusts accordingly with these operations.

6. **Stack Frame (Activation Record)**
   - Each function call leads to the creation of a stack frame on the stack. This frame contains:
     - **Return Address (`ra`)**: Directs the program where to return after the function completes.
     - **Return Value Space**: Reserved for any value the function returns (if it's not a `void` function).
     - **Actual Parameters (Arguments)**: The values passed to the function.
     - **Local Variables**: Variables only used within the function.

7. **Stack(runtime or call) vs. Heap**
   - Memory contains two main sections managed at runtime: the **stack** and the **heap**. The heap is for dynamic memory allocation.
   - They often grow towards one another. A "stack overflow" error occurs if they meet.
   - Stack growth direction varies with architectures. On x86 (common in PCs), it grows towards address zero.

The stack (or Call Stack) is where function calls, local variables, return addresses, and other related information are stored. It operates in a Last-In, First-Out (LIFO) manner, meaning the last function called is the first to be finished and removed from the stack.

The heap is a different part of memory used for dynamic memory allocation. For example, when you allocate memory for an object or array during runtime (as opposed to compile-time), it's usually stored on the heap.

### Program Memory Visualization

+--------------------------+
|      Runtime Stack       |
|   (Stack Segment - SS)   |
|            ↓             |
+--------------------------+
|            ↑             |
|          Heap            |
+--------------------------+
|   Uninitialized Data     |
|           (BSS)          |
+--------------------------+
| Initialized Data Segment |
+--------------------------+
|      Code Segment        |
+--------------------------+


1. **Runtime Stack (Stack Segment - SS)**: This is where function call information, local variables, return addresses, and other stack-related data are stored. The stack typically starts from a high memory address and grows downwards as more function calls are added.

2. **Heap**: The heap is used for dynamic memory allocation. When your program needs memory during runtime (e.g., when you use functions like `malloc` in C), the memory is allocated from the heap. The heap starts from a lower address compared to the stack and grows upwards as more memory is dynamically allocated.

3. **Uninitialized Data (BSS)**: This segment contains uninitialized global and static variables. The BSS is essentially a part of the data segment specific to uninitialized values.

4. **Initialized Data Segment**: Contains global and static variables that have been initialized with a value.

5. **Code Segment**: Contains the executable instructions of the program.

The arrows between the Heap and the Runtime Stack show their respective growth directions. If they grow too much (e.g., too much recursion or too much dynamic memory allocation), they can collide, leading to issues like stack overflow.

In summary, this picture provides a conceptual overview of the memory layout of a running program. It helps one understand where different types of data and instructions are stored and how memory is managed during program execution.



