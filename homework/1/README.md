📌 Homework 1 - Assembly Program Explanation
🔍 Program Overview
This program is written in ARM Assembly and demonstrates branching and iteration using a structured loop. The goal of the program is to increment the value in register r0 by 2 repeatedly until it reaches the target value stored in r1. Once r0 matches r1, the program terminates using a system call.
🛠️ How the Program Works
Step-by-Step Execution:
1. Register Initialization:
    * mov r0, #2 → Initializes r0 to 2.
    * mov r1, #10 → Sets r1 as the target value (10).
2. Loop Execution:
    * cmp r0, r1 → Compares r0 and r1.
    * beq step10 → If r0 == r1, the program branches to termination.
    * add r0, r0, #2 → If the condition is not met, r0 is incremented by 2.
    * b step1 → The program unconditionally jumps back to re-check the condition.
3. Program Termination:
    * mov r7, #1 → Loads Linux syscall number for exit into r7.
    * svc #0 → Executes the system call, terminating the program.
⚠️ Issues in the Original Code
Problems Identified:
❌ Redundant Instructions: The original version manually increments r0 multiple times instead of using a loop. ❌ Lack of Scalability: If we want to change r1, multiple lines need manual modification. ❌ Inefficient Execution: The program does not leverage iteration, making it less optimized.
✅ How I Improved the Code (Using Branching & Iteration)
To optimize the code, I introduced structured looping and conditional branching:
Enhancements Made:
1️⃣ Introduced a Loop:
* Instead of manually adding 2 multiple times, I replaced redundant operations with a looping mechanism.
2️⃣ Utilized Conditional Branching:
* The program now checks r0 < r1 using cmp and branches accordingly without unnecessary instructions.
3️⃣ Optimized System Call Handling:
* Instead of using svc #0 directly, I implemented the proper Linux syscall (mov r7, #1 and svc #0) to ensure correct program termination.
4️⃣ Improved Readability & Maintainability:
* The revised version allows easy modifications (e.g., changing r1 to another number only requires modifying one line).
🚀 Optimized Approach Using Branching & Iteration
Updated Program Flow:
🔹 Set r0 = 2 and r1 = 10. 🔹 Enter a loop, where r0 increments by 2 per iteration. 🔹 If r0 == r1, the program jumps to the termination routine. 🔹 If not, it loops again. 🔹 Efficient, scalable, and follows best practices.
📂 Code Implementation - homework-1-solution.s
# Optimized ARM Assembly Code with Looping and Branching
# This program demonstrates an efficient way to increment a value stored in r0 by 2
# until it reaches a target value stored in r1. The program uses a loop structure,
# avoiding redundant instructions and improving scalability.

.global _start  # Define the global entry point for the program

_start:
    mov r0, #2      @ Initialize r0 with the starting value (2)
    mov r1, #10     @ Set r1 to the target value (10)
    
# Step 1: Check if r0 has reached the target value
step1:
    cmp r0, r1      @ Compare the current value of r0 with r1
    beq step10      @ If r0 == r1, branch to termination step
    
# Step 2: Increment r0 in steps of 2 and loop back for comparison
step2:
    add r0, r0, #2  @ Increment r0 by 2 to progress toward r1
    b step1         @ Unconditionally branch back to step1 for comparison

# Step 10: Termination process using a system call
step10:
    mov r7, #1      @ Load r7 with syscall number 1 (exit syscall for Linux)
    svc #0          @ Perform a system call to exit the program

📌 Final Thoughts
This optimized implementation ensures better efficiency, modularity, and maintainability, making it a scalable solution that adheres to best practices in ARM Assembly. 🚀

