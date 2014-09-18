03_Queue_Lab
============

Implement an array-based queue in C++

Note: When you create your project, do NOT add ArrayQueue.ipp to the list of source files, add it to the list of include files. You will see that ArrayQueue.ipp is #included at the bottom of ArrayQueue.h. See ArrayQueue.h for more explanation.

Requirements
------------

1. remove takes O(1) time
2. add takes O(1) time, unless it calls grow (in that case O(n) is okay)
3. grow is only called if the number of items == backingArraySize, and the size of the array is doubled during grow
4. grow takes O(n) time
5. Do not leak memory (make sure grow and the destructor do the right thing)
6. getNumItems is O(1) time
7. add and remove throw excpetions as appropriate
8. You must use the array in a circular fashion. If you don't do this you probably won't be able to get #1, #2 and #3 to all be true.

Reading
=======
"Open Data Structures," Chapter 2, up through section 2.4 (ArrayDequeue). http://opendatastructures.org/ods-cpp/2_Array_Based_Lists.html

Information about the Von Neumann computing model may be helpful. This optional reading is section 2.2 of "Algorithms and Data Structures: A Basic Toolbox" by Melhorn and Sanders. A free copy may be found here: http://www.mpi-inf.mpg.de/~mehlhorn/ftp/Toolbox/Introduction.pdf

Questions
=========

#### 1. Which of the above requirements work, and which do not? For each requirement, write a brief response.

1. Yes, remove costs O(1). It makes sure numItems isn't 0, then deletes and returns the first item in the queue.
2. Yes, add is O(1) or O(n) when it calls grow(). The method simply adds a new object to the queue, no shifting necessary.
3. This is true in my code, grow doubles the backingArraySize and is only called from ArrayQueue.ipp when called from the add method, when numItems == backingArraySize.
4. Yes, my grow method doubles the backingArraySize and iterates through the queue to copy it back into a new array of double the size.
5. My program deletes memory at all appropriate times.
6. Of course, it's only one line. It's just a getter.
7. Add checks the size before adding to possibly call grow, and remove may throw an exception when no elements are left to delete.
8. Yes, my array is used in a circular fashion. My program can easily remove and add items quickly, without any unnecessary sorting or iteration.

#### 2. If we did a Stack instead of a Queue, which of the private methods and variables would we need to keep, and which could we get rid of? Explain your answer.
Of the private methods and variables, we would need backingArray, numItems (for the length), and grow(), but we could get rid of front and backingArraySize. We still need the array and its size, but not the first element as that will not change unless the array is empty, and the backingArraySize would be the same as numItems. The grow() operation is needed for all arrays to resize if they can't on their own.

#### 3. What is one question that confused you about this exercise, or one piece of advice you would share with students next semester?
I didn't understand the mechanics of pointing to a virtual array rather than actually instantiating an array in the program. I understand them now, but I didn't really get what to do with backingArraySize vs numItems and front until halfway through the program.

#### 4. In Java you might write "class ArrayQueue extends Queue" ... how do you write the same thing in C++?
class ArrayQueue : class Queue

#### 5. What is the purpose of "templates" in C++?
Templates allow classes to use objects of any valid type.

#### 6. What would the syntax be for dynamically allocating an array of 10 ints, in C++?
int *ray = new int[10];

#### 7. What is the purpose of a class destructor in C++? Why don't you need them in Java?
In c++, memory is stored in pointers for each variable, unlike in Java. When a variable isn't being used any more, a c++ program should delete this memory to free space. In Java, pointers don't use a noticable amount of space in the computer while the program is running.