# 🚀 Complete Operating Systems (OS) Crash Course for Interviews

> Prepared for rapid understanding and retention in 5-6 hours. Includes theory + examples + analogies.

---

## 📘 Table of Contents

1. What is an Operating System?
2. Processes vs Threads
3. CPU Scheduling Algorithms
4. Memory Management
5. Deadlock
6. Concurrency & Synchronization
7. File Systems
8. Virtual Memory & Paging
9. System Calls & Context Switching
10. Practice Questions

---

## 1️⃣ What is an Operating System?

### 📌 Definition:
An **Operating System (OS)** is a software that acts as an **intermediary between user and hardware**. It manages system resources and provides services to applications.

### 🧠 Key Functions:
- Process Management
- Memory Management
- File System Handling
- Device Management
- Security and Access Control

### 💡 Example:
When you run a code editor, OS loads it into memory, allocates CPU time, and manages input/output with disk and keyboard.

---

## 2️⃣ Processes vs Threads

### 🔹 Process:
- A program in execution
- Has **separate memory space**
- Independent from other processes

### 🔹 Thread:
- A **lightweight process**
- Shares memory with other threads in same process
- Ideal for multitasking

### 🧠 Analogy:
- Process = Chrome Browser
- Threads = Tabs inside Chrome

### 📍 Example:
In a music app:
- One thread plays music
- One thread handles UI
- One thread downloads album art

---

## 3️⃣ CPU Scheduling Algorithms

Scheduling determines which process gets the CPU next.

### 🔸 FCFS (First Come First Serve):
- Like a queue at a bank
- Non-preemptive
- Once a process starts executing, it runs until it completes, even if another process arrives while it's running
- one of the easiest CPU scheduling algorithms to understand and implement

### 🔸 SJF (Shortest Job First):
- Executes the job with shortest burst time
- May cause starvation
- [[Great question! Let's break it down.

> **"May cause starvation"** — in the context of **Shortest Job First (SJF) scheduling**, this means:

#### 🧠 Starvation Explained:
If **shorter processes keep arriving**, the **longer processes may never get scheduled**, because the scheduler always picks the shortest job.

#### 🔸 Example:
Let’s say we have one long job `P1` (burst time 20ms), and a bunch of small jobs `P2, P3, P4...` (each 1ms) keep arriving continuously.

- SJF always picks the shortest one first.
- So `P1` keeps waiting... and waiting...
- It **starves** — never gets CPU time.

This is called **starvation**, a form of **indefinite blocking**.]]


### 🔸 Round Robin:
- Each process gets equal time (quantum)
- Preemptive -> scheduler can interrupt a process and switch to another process after the time quantum expires
- each process receives an equal, fixed amount of time (the "quantum") to execute before being preempted and moved to the back of the ready queue.
- This ensures fairness and allows all processes to get a chance to run.

### 🔸 Priority Scheduling:
- Higher priority runs first
- Can be preemptive or non-preemptive

### 📍 Example:
Imagine 3 tasks arriving:
```
P1 (BT=4)   P2 (BT=2)   P3 (BT=1)
```
In FCFS: P1 → P2 → P3

In SJF:  P3 → P2 → P1

---

## 🧠 **Memory Management in OS**
Memory management is **how the operating system (OS)** handles and organizes the computer’s memory (RAM).  
Think of RAM as your study table. The OS decides **what goes where**, **how much space each item gets**, and **cleans up** when it’s not needed anymore.

---

### 📌 **Main Responsibilities of Memory Management**
1. **Keep Track of Memory Usage**  
   The OS needs to know which parts of RAM are being used and which are free.  
   Example: Like a hotel manager knows which rooms are occupied.

2. **Allocate/Deallocate Memory**  
   When a program starts, the OS gives it memory. When the program ends, the memory is freed.  
   Example: Giving someone a room when they check in, and cleaning it after they leave.



## 🔸 **Paging**
**Paging** breaks memory into **fixed-size blocks** called **pages**.

- **Why?**  
  To avoid **external fragmentation** (i.e., small gaps of unusable memory).
  
- **How?**  
  🔹 Memory (RAM) is divided into equal-sized **frames**  
  🔹 Processes are divided into equal-sized **pages**  
  🔹 The OS uses a **page table** to map logical addresses (used by the program) to physical addresses (actual location in RAM).

### 🧾 Example:
Imagine RAM is a bookshelf with fixed-sized slots (frames).  
You have a book (process) split into chapters (pages).  
The OS keeps a **table** to remember which chapter is in which slot.



## 🔸 **Segmentation**
**Segmentation** divides memory into **logical units** (not fixed-size).  
Examples: code, data, stack, heap — each gets its own segment.

- **Why?**  
  It reflects the way programs are logically structured.  
  You can have different-sized segments instead of fixed-sized pages.

- **How?**  
  Each segment has a **base address** (starting point) and a **limit** (size).  
  The OS maintains a **segment table**.

- **Drawback:**  
  Can cause **fragmentation**, because segments are of variable sizes.



### 🧠 Difference between Paging and Segmentation:

| Feature        | Paging                      | Segmentation                   |
|----------------|-----------------------------|---------------------------------|
| Division       | Fixed-size pages             | Variable-size segments          |
| Mapping        | Page table                   | Segment table                   |
| Fragmentation  | Avoids **external**          | Can cause **external**          |
| Flexibility    | Less (uniform blocks)        | More (logical structure)        |



## 📍 **Real-Life Example: Opening Browser Tabs**

Let’s say you open multiple tabs in Chrome:

- Each tab is a **process** or a **thread**.
- OS allocates a **page** for each tab in memory.
- It keeps a **page table** to track which tab’s memory is stored where in RAM.

So, if Tab 1 crashes, it doesn’t affect Tab 2 — because each has its own separate memory block.


---

## 5️⃣ Deadlock

### 📌 What is Deadlock?
A state where **two or more processes are waiting for each other** to release resources.

### 🔸 Four Conditions (Coffman):
1. Mutual Exclusion
2. Hold and Wait
3. No Preemption
4. Circular Wait

### 🔸 Solutions:
- **Avoidance**: e.g., Banker’s algorithm
- **Detection and Recovery**
- **Prevention**: Break at least one Coffman condition

### 🧠 Analogy:
Two people face each other in a narrow hallway, each waiting for the other to move.

---

## 6️⃣ Concurrency & Synchronization

### 🔸 Problem:
When multiple threads/processes access **shared resources**, inconsistency can occur.

### 🔹 Race Condition:
Output depends on **timing/order of execution**

### 🔹 Critical Section:
Portion of code accessing shared resource

### 🔹 Semaphores:
A synchronization tool to manage access to critical section

```c
semaphore S = 1;
wait(S);
   // critical section
signal(S);
```

### 📍 Example:
Two people editing the same Google doc paragraph without coordination = mess.

---

## 7️⃣ File System

### 📌 Role of File System:
- Manages how data is stored and retrieved
- Provides abstraction (filenames vs physical disk sectors)

### 🔸 Concepts:
- **Inode**: Metadata about file (size, location)
- **File Descriptor**: Handle to access file
- **Directory**: Special file that maps names to inodes

### 📍 Example:
Like a book index → points to page number → actual content

---

## 8️⃣ Virtual Memory & Paging

### 🔹 Virtual Memory:
Lets you run programs **larger than actual RAM** using disk as backup

### 🔹 Paging with Virtual Memory:
- Logical address split into **Page Number + Offset**
- Uses **page tables** to translate logical to physical addresses

### 🔹 Page Replacement Algorithms:
- **FIFO**: Oldest page replaced
- **LRU**: Least recently used page replaced
- **Optimal**: Replace page not used for longest time (ideal)

---

## 9️⃣ System Calls & Context Switching

### 🔸 System Call:
Interface to request OS services (e.g., `open()`, `read()`, `write()`)

### 🔸 Context Switch:
When CPU switches from one process to another
- Saves current state (PCB)
- Loads new process’s state

### 📍 Example:
Switching TV channels – saving one show’s state and loading another

---

## 🔟 OS Interview Practice Questions

### ✅ Theory-Based:
1. Difference between process and thread?
2. What are the advantages of paging?
3. What causes deadlock?
4. How is memory managed in OS?
5. Explain semaphores with example.

### ✅ Scenario-Based:
1. How would you avoid race conditions?
2. Describe a real-world example of a deadlock.
3. What happens during a context switch?

---

## 🏁 Conclusion
This is your fast-track to OS mastery. Use real-life analogies + revise theory + practice Q&A. Let me know when you're ready for Networking — and I’ll build that the same way!

