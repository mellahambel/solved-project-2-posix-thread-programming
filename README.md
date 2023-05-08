Download Link: https://assignmentchef.com/product/solved-project-2-posix-thread-programming
<br>
<h1>Introduction</h1>

The purpose of this project is to practice Pthread programming by solving various problems. The objectives of this project is to:

<ol>

 <li>Get familiar with Pthread creation and termination.</li>

 <li>Learn how to use mutexes and conditional variables in Pthread.</li>

 <li>Learn how to design efficient solutions for mutual exclusion problems.</li>

</ol>

<h1>Project submission</h1>

For each project, please create a zipped file containing the following items, and submit it to Canvas.

<ol>

 <li>A report that includes (1) the (printed) full names of the project members, and the statement: <strong>We have neither given nor received unauthorized assistance on this work</strong>; (2) the name of your virtual machine (VM), and the password for the instructor account (details see <em>Accessing VM </em>below); and (3) a brief description about how you solved the problems and what you learned. The report can be in txt, doc, or pdf format.</li>

 <li>The Pthread code and files that contain your test cases.</li>

</ol>

<em>Accessing VM. </em>Each team should specify the name of your VM that the instructor can login to check the project results. Please create a new user account called instructor in your VM, and place your code in the home directory of the instructor account (i.e., /home/instructor). Make sure the instructor has the appropriate access permission to your code. In your project report, include your password for the instructor account.

<h1>Tasks</h1>

<h2>Task 1 (30 points)</h2>

Given two character strings s1 and s2. Write a Pthread program to find out the number of substrings, in string s1, that is exactly the same as s2. For example, if number substring(s1, s2) implements the function, then you have number substring(‘‘abcdab”, ‘‘ab”) = 2, number substring(‘‘aaa”, ‘‘a”) = 3, and number substring(‘‘abac”, ‘‘bc”) = 0. The size of s1 and s2 (n1 and n2), as well as their data are the input by the user, via a file.

Assume that n1 is at least twice as long as n2.

Attached code substring sequential.c is a sequential solution of the problem. read f() reads the two strings from a file named string.txt, and num substring() calculates the number of substrings. Write a parallel program using Pthread based on this sequential solution.

HINT: Strings s1 and s2 are stored in a file named string.txt. String s1 is partitioned among NUM THREADS threads to concurrently search for matching with string s2. After a thread finishes its work and obtains the number of local matchings, this local number is added into a global variable showing the total number of matched substrings in string s1. Finally, this total number is printed out. You can find an example of the file string.txt in the attached source code.

MORE HINT: If you partition s1 among threads, you will miss those s2’s at the partition boundaries. Instead of partitioning the data, can you partition the task(s)?

<h2>Task 2 (30 points)</h2>

Use <em>condition variables </em>to solve a producer-consumer problem. Here we have two threads: one producer and one consumer. The producer reads characters one by one from a string stored in a file named message.txt, then writes sequentially these characters into a circular queue. Meanwhile, the consumer reads sequentially from the queue and prints them in the same order. Assume a buffer (queue) size of 6 characters. Write a Pthread program using condition variables.

<h2>Task 3 (40 points)</h2>

Read attached code list-forming.c and modify the program to improve its performance. In this program there are num threads threads. Each thread creates a data node and attaches it to a global list. This operation is repeated K times by each thread. The performance of this program is measured by the program runtime (in microsecond). Apparently, the operation of attaching a node to the global list needs to be protected by a lock and the time to acquire the lock contributes to the total run time. Try to modify the program in order to reduce the program runtime.

<h3>Your tasks</h3>

<ol>

 <li>Implement a modified version of list-forming.c and name it my list-forming.c.</li>

 <li>Verify that your program achieves better performance than the original version by using different combinations of K and num threads. Typical values of K could be 200, 400, 800, … Typical values of num threads could be 2, 4, 8, 16, 32, 64, … Draw diagrams to show the performance trend.</li>

 <li>In the report, explain your design and discuss the performance results.</li>

</ol>

HINTS:

<ol>

 <li>Since the problem does not require a specific order of the nodes in the global list, there are two ways to add nodes. First, a node could be added to the global list immediately after it is created by a thread. Alternatively, a thread could form a local list of K nodes and add the local list to the global list in one run. Will the choice in how to add nodes make a difference? Why?</li>

 <li>The original program uses pthread mutex trylock. Will the use of pthread mutex lock make a difference? Why?</li>

 <li>Each thread is pinned to a specific CPU (according to the thread id). Will letting threads run on all CPUs make a difference? Why?</li>

</ol>

<h3>Instructions</h3>

<ol>

 <li>Power off your VM and change to VM setting to use 4 virtual CPUs.</li>

 <li>Verify that you VM has 4 virtual CPUs:</li>

</ol>

$ cat /proc/cpuinfo

You should see information about 4 CPUs (processor: 0-3).

<ol start="3">

 <li>To compile the program:</li>

</ol>

<table width="576">

 <tbody>

  <tr>

   <td width="576">$gcc list-forming.c -o list-forming -pthread -D GNU SOURCE</td>

  </tr>

 </tbody>

</table>


