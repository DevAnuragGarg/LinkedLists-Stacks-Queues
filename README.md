# LinkedLists-Stacks-Queues

What is Data Structures: A data structure is a way of organizing the data so that the data can be used efficiently. Different kinds of data structures are suited to different kinds of applications, and some are highly specialized to specific tasks.

======
What are linear and non linear data Structures
Linear: A data structure is said to be linear if its elements form a sequence or a linear list. Examples: Array. Linked List, Stacks and Queues. Non-Linear: A data structure is said to be non-linear if traversal of nodes is nonlinear in nature. Example: Graph and Trees.

======
How is an Array different from Linked List?
1) The size of the arrays is fixed, Linked Lists are Dynamic in size.
2) Inserting and deleting a new element in an array of elements is expensive, Whereas both insertion and deletion can easily be done in Linked Lists.
3) Random access is not allowed in Linked Listed.
4) Extra memory space for a pointer is required with each element of the Linked list.
5) Arrays have better cache locality that can make a pretty big difference in performance. Array access time is spacial locality in memory, means they are continuous block of memory, so array element will be physically near. This greatly benefits from modern CPU caching methods.
6) In an array, memory is assigned during compile time while in a Linked list it is allocated during execution or runtime.

======
Advantage and Disadvantages of Doubly LinkedList : We can navigate in both the directions. In Singly linked list we cannot remove the node unless we don't have the address of predecessor. But in doubly linked list we can delete a node even if we don't have previous nodes address as previous node address is already present in the node's left pointer. Each node of DLL required extra pointer. Each insertion or deletion is bit headache as more pointer operations.

======
Circular linked list: Linked list having last node having address of header. No pointer is pointing to null. Every node has a successor. Ex. When several processes are using CPU for same amount of time, we have to sure no new process should access the CPU before earlier processes gets finished. Circular linked list is a linked list where all nodes are connected to form a circle. There is no NULL at the end. A circular linked list can be a singly circular linked list or doubly circular linked list.

======
Advantages of Circular Linked Lists:
1) Any node can be a starting point. We can traverse the whole list by starting from any point. We just need to stop when the first visited node is visited again.
2) Useful for implementation of queue. Unlike this implementation, we don’t need to maintain two pointers for front and rear if we use circular linked list. We can maintain a pointer to the last inserted node and front can always be obtained as next of last.
3) Circular lists are useful in applications to repeatedly go around the list. For example, when multiple applications are running on a PC, it is common for the operating system to put the running applications on a list and then to cycle through them, giving each of them a slice of time to execute, and then making them wait while the CPU is given to another application. It is convenient for the operating system to use a circular list so that when it reaches the end of the list it can cycle around to the front of the list.
4) Circular Doubly Linked Lists are used for implementation of advanced data structures like Fibonacci Heap.

======
Spatial vs Temporal Locality
A sequence of references is said to have spatial locality if things that are referenced close in time are also close in space (nearby memory addresses, nearby sectors on a disk, etc.). A sequence is said to have temporal locality if accesses to the same thing are clustered in time. If a program accesses every element in a large array and reads it once and then moves on to the next element and does not repeat an access to any given location until it has touched every other location then it is a clear case of spatial locality but not temporal locality. On the other hand, if a program spends time repeatedly accessing a random subset of the locations on the array before moving on to another random subset it is said to have temporal locality but not spatial locality. A well written program will have data structures that group together things that are accessed together, thus ensuring spatial locality. If you program is likely to access B soon after it accesses A then both A and B should be allocated near each other. Your first example: A[0][1], A[0][2], A[0][3] shows spatial locality, things that are accessed close in time are close in space. It does not show temporal locality because you have not accessed the same thing more than once. Your second example: A[1], A[2], A[3] also shows spatial locality, but not temporal locality. Here's an example that shows temporal locality A[1], A[2000], A[1], A[1], A[2000], A[30], A[30], A[2000], A[30], A[2000], A[30], A[4], A[4]

======
Program for n’th node from the end of a Linked List
- Calculate the length of Linked List. Print the (len – n + 1)th node from the beginning of the Linked List.
- Maintain two pointers – reference pointer and main pointer. Initialize both reference and main pointers to head. First move reference pointer to n nodes from head. Now move both pointers one by one until reference pointer reaches end. Now main pointer will point to nth node from the end. Return main pointer.

======
Reverse a linked list: 
- Iterate trough the linked list. In loop, change next to prev, prev to current and current to next.
- Recursive Method: Divide the list in two parts - first node and rest of the linked list. Call reverse for the rest of the linked list. Link rest to first. Fix head pointer
private fun reverseLinkedList(node: LLNode<T>): LLNode<T> {
    return if (node.nextNode != null) {
        val newNode = reverseLinkedList(node.nextNode!!)
        newNode.nextNode = node
        node.nextNode = null
        node
    } else {
        headNode = node
        node
    }
}

======
Detect loop in a linked list:
- Traverse the list one by one and keep putting the node addresses in a Hash Table. At any point, if NULL is reached then return false and if next of current node points to any of the previously stored nodes in Hash then return true.
- Mark Visited Nodes: This solution requires modifications to basic linked list data structure.  Have a visited flag with each node.  Traverse the linked list and keep marking visited nodes.  If you see a visited node again then there is a loop. This solution works in O(n) but requires additional information with each node.
- Floyd’s Cycle-Finding Algorithm: This is the fastest method. Traverse linked list using two pointers.  Move one pointer by one and other pointer by two.  If these pointers meet at some node then there is a loop.  If pointers do not meet then linked list doesn’t have loop. Time Complexity: O(n) Auxiliary Space: O(1)
	
======
Write a function to get the intersection point of two Linked Lists.
- Use 2 nested for loops. Outer loop will be for each node of the 1st list and inner loop will be for 2nd list. In the inner loop, check if any of nodes of 2nd list is same as the current node of first linked list. Time complexity of this method will be O(m*n) where m and n are the number of nodes in two lists.
- This solution requires modifications to basic linked list data structure. Have a visited flag with each node. Traverse the first linked list and keep marking visited nodes. Now traverse second linked list, If you see a visited node again then there is an intersection point, return the intersecting node. This solution works in O(m+n) but requires additional information with each node
- Using difference of nodes: Get count of the nodes in first list, let count be c1. Get count of the nodes in second list, let count be c2. Get the difference of counts d = abs(c1 – c2) Now traverse the bigger list from the first node till d nodes so that from here onwards both the lists have equal no of nodes. Then we can traverse both the lists in parallel till we come across a common node. (Note that getting a common node is done by comparing the address of the nodes)
- Traverse the first linked list(count the elements) and make a circular linked list. (Remember last node so that we can break the circle later on). Now view the problem as find the loop in the second linked list. So the problem is solved. Since we already know the length of the loop(size of first linked list) we can traverse those many number of nodes in second list, and then start another pointer from the beginning of second list. we have to traverse until they are equal, and that is the required intersection point. Remove the circle from the linked list.
- (Traverse both lists and compare addresses of last nodes) This method is only to detect if there is an intersection point or not.
- Basically we need to find common node of two linked lists. So we hash all nodes of first list and then check second list. Create an empty hash table such that node address is used as key and a binary value present/absent is used as value. Traverse the first linked list and insert all nodes’ addresses in hash table. Traverse the second list. For every node check if it is present in hash table. If we find a node in hash table, return the node.
- Using stacks. Pushing 1st linked list in stack 1 and second linked list in stack 2. Start popping out simultaneously. Whenever the value is different before that the node which is popped out is the intersection node of two linked lists.

======
Function to check if a singly linked list is palindrome
- Traverse the given list from head to tail and push every visited node to stack. Traverse the list again. For every visited node, pop a node from stack and compare data of popped node with currently visited node. If all nodes matched, then return true, else false.
- Get the middle of the linked list. Reverse the second half of the linked list. Check if the first half and second half are identical. Construct the original linked list by reversing the second half again and attaching it back to the first half
	
======
Detect and Remove Loop in a Linked List
- We know that Floyd’s Cycle detection algorithm terminates when fast and slow pointers meet at a common point. We also know that this common point is one of the loop nodes. We store the address of this in a pointer variable say ptr2. Then we start from the head of the Linked List and check for nodes one by one if they are reachable from ptr2. When we find a node that is reachable, we know that this node is the starting node of the loop in Linked List and we can get pointer to the previous of this node.
- Detect Loop using Floyd’s Cycle detection algorithm and get the pointer to a loop node. Count the number of nodes in loop. Let the count be k. Fix one pointer to the head and another to kth node from head. Move both pointers at the same pace, they will meet at loop starting node. Get pointer to the last node of loop and make next of it as NULL.
- We do not need to count number of nodes in Loop. After detecting the loop, if we start slow pointer from head and move both slow and fast pointers at same speed until fast don’t meet, they would meet at the beginning of the loop.
	
=====
Josephus Circle using circular linked list: There are n people standing in a circle waiting to be executed. The counting out begins at some point in the circle and proceeds around the circle in a fixed direction. In each step, a certain number of people are skipped and the next person is executed. The elimination proceeds around the circle (which is becoming smaller and smaller as the executed people are removed), until only the last person remains, who is given freedom. Given the total number of persons n and a number m which indicates that m-1 persons are skipped and m-th person is killed in circle. The task is to choose the place in the initial circle so that you are the last one remaining and so survive.
Create a circular linked list of size n. Traverse through linked list and one by one delete every m-th node until there is one node left. Return value of the only left node.

=====
Remove duplicates from an unsorted linked list
- Using two loops
- Sorting and then removing duplicated from sorted list
- Using hashing

=====
Sorting a linked list: Merge sort is often preferred for sorting a linked list. The slow random-access performance of a linked list makes some other algorithms (such as quicksort) perform poorly, and others (such as heap sort) completely impossible.

private Node mergeSortLinkList(Node startNode){
	//Break the list until list is null or only 1 element is present in List.
	if(startNode==null || startNode.getNext()==null){
		return startNode;
	}
	//Break the linkList into 2 list.
	//Finding Middle node and then breaking the Linked list in 2 parts.
	//Now 2 list are, 1st list from start to middle and 2nd list from middle+1 to last.
	Node middle = getMiddle(startNode);
	Node nextOfMiddle = middle.getNext();
	middle.setNext(null);

	//Again breaking the List until there is only 1 element in each list.
	Node left = mergeSortLinkList(startNode);
	Node right = mergeSortLinkList(nextOfMiddle);

	//Once complete list is divided and contains only single element, 
	//Start merging left and right half by sorting them and passing Sorted list further. 
	Node sortedList = mergeTwoListRecursive(left, right);
	return sortedList;
}

//Recursive Approach for Merging Two Sorted List
private Node mergeTwoListRecursive(Node leftStart, Node rightStart){
	if(leftStart==null)
		return rightStart;
	if(rightStart==null)
		return leftStart;
	Node temp=null;
	if(leftStart.getData()<rightStart.getData()){
		temp=leftStart;
		temp.setNext(mergeTwoListRecursive(leftStart.getNext(), rightStart));
	}else{
		temp=rightStart;
		temp.setNext(mergeTwoListRecursive(leftStart, rightStart.getNext()));
	}
	return temp;
}

private Node getMiddle(Node startNode) {
	if(startNode==null){
		return startNode;
	}
	Node pointer1=startNode;
	Node pointer2=startNode;
	while(pointer2!=null && pointer2.getNext()!=null && pointer2.getNext().getNext()!=null){
		pointer1 = pointer1.getNext();
		pointer2 = pointer2.getNext().getNext();
	}
	return pointer1;
}

======	
Given only a pointer/reference to a node to be deleted in a singly linked list, how do you delete it?
- Copy the data from the next node to the node to be deleted and delete the next node. This solution doesn’t work if the node to be deleted is the last node of the list.

======	
Search for an element: you can do this recursively or iteratively.

======	
Add 1 to a number represented as linked list: 1999 is represented as (1-> 9-> 9 -> 9) and adding 1 to it should change it to (2->0->0->0)
- Reverse linked list and then add 1 and carry forward the 1
- Get the integer value, add 1 and then put the value in the linked list
	
=====
Point arbitrary pointer to greatest value right side node in a linked list: singly linked list with every node having an additional “arbitrary” pointer that currently points to NULL
- Reverse given linked list, Start traversing linked list and store maximum value node encountered so far. Make arbitrary of every node to point to max. If the data in current node is more than max node so far, update max. Reverse modified linked list and return head.
	
=====
Sort linked list which is already sorted on absolute values
- Traverse the linked list from beginning to end. For every visited node, check if it is out of order. If it is, remove it from its current position and insert at correct position. This is implementation of insertion sort for linked list and time complexity of this solution is O(n*n).
- An efficient solution can work in O(n) time. An important observation is, all negative elements are present in reverse order. So we traverse the list, whenever we find an element that is out of order, we move it to the front of linked list.
	
=====
Union and Intersection of two linked lists
- Initialize result list as NULL. Traverse list1 and look for its each element in list2, if the element is present in list2, then add the element to result. Similar for union
- Merge Sort: Sort the first Linked List using merge sort. This step takes O(mLogm) time. Sort the second Linked List using merge sort. This step takes O(nLogn) time. Linearly scan both sorted lists to get the union and intersection. This step takes O(m + n) time. 
- Hashing: Initialize the result list as NULL and create an empty hash table. Traverse both lists one by one, for each element being visited, look the element in hash table. If the element is not present, then insert the element to result list. If the element is present, then ignore it.
	
=====
Rearrange a given list such that it consists of alternating minimum maximum elements
- The idea is to sort the list in ascending order first. Then we start popping elements from the end of the list and insert them into their correct position in the list.
	
=====
Count pairs from two linked lists whose sum is equal to a given value
- (Naive Approach): Using two loops pick elements from both the linked lists and check whether the sum of the pair is equal to x or not.
- (Sorting): Sort the 1st linked list in ascending order and the 2nd linked list in descending order using merge sort technique. 
- (Hashing): We store all first linked list elements in hash table. For elements of second linked list, we subtract every element from x and check the result in hash table. If result is present, we increment the count.

=====
Count rotations in sorted and rotated linked list
- reverse singly linked list to check condition whether current node value is greater than value of next node. If the given condition is true, then break the loop

=====	
Sort a linked list of 0s, 1s and 2s
- Traverse the list and count the number of 0s, 1s and 2s. Let the counts be n1, n2 and n3 respectively. Traverse the list again, fill the first n1 nodes with 0, then n2 nodes with 1 and finally n3 nodes with 2.
- Create 3 linked lists and attach them later after adding
	
=====
Find the sum of last n nodes of the given Linked List
- Recursive approach using system call stack
- Iterative approach using user defined stack
- Reversing the linked list
- Using length of linked list(length-n)
- Use of two pointers requires single traversal
- First move reference pointer to n nodes from head and while traversing accumulate node’s data to some variable, say sum. Now move both pointers simultaneously until reference pointer reaches to the end of the list
	
=====
Merge two sorted linked lists such that merged list is in reverse order
- Reverse list a. Reverse list b. Merge both.
- Merge both the list and reverse them
- Create a new list while traversing both the lists
	
======
Check whether the length of given linked list is Even or Odd
- Linearly check that
- Increase the 2 steps at a time
	
======
Add two numbers in linked list
- check the length of the linked lists. Make the length of the linked list equal by adding 0 as the value for the new node whose length is less. Then reverse the linked list and keep adding the values. You have reverse the linked list because you cannot get the last element and add the values (direction of the linked list)

=====
Can doubly linked be implemented using a single pointer variable in every node?
Doubly linked list can be implemented using a single pointer. See XOR Linked List – A Memory Efficient Doubly Linked List

======
ADOBE Interview Question
XOR Linked List : Memory efficient Doubly Linked List: An ordinary Doubly Linked List requires space for two address fields to store the addresses of previous and next nodes. A memory efficient version of Doubly Linked List can be created using only one space for address field with every node. This memory efficient Doubly Linked List is called XOR Linked List or Memory Efficient as the list uses bitwise XOR operation to save space for one address. In the XOR linked list, instead of storing actual memory addresses, every node stores the XOR of addresses of previous and next nodes.
XOR List Representation: Let us call the address variable in XOR representation npx (XOR of next and previous)
Node A: npx = 0 XOR add(B) // bitwise XOR of zero and address of B
Node B: npx = add(A) XOR add(C) // bitwise XOR of address of A and address of C
Node C: npx = add(B) XOR add(D) // bitwise XOR of address of B and address of D
Node D: npx = add(C) XOR 0 // bitwise XOR of address of C and 0
Traversal of XOR Linked List: We can traverse the XOR list in both forward and reverse direction. While traversing the list we need to remember the address of the previously accessed node in order to calculate the next node’s address. For example when we are at node C, we must have address of B. XOR of add(B) and npx of C gives us the add(D). The reason is simple: npx(C) is “add(B) XOR add(D)”. If we do XOR of npx(C) with add(B), we get the result as “add(B) XOR add(D) XOR add(B)” which is “add(D) XOR 0” which is “add(D)”. So we have the address of next node.

====================
STACKS
====================
STACK: Stack is a linear data structure which the order LIFO(Last In First Out) or FILO(First In Last Out) for accessing elements. Basic operations of stack are : Push, Pop ,Peek. Applications of Stack:
1) Infix to Postfix Conversion using Stack
2) Evaluation of Postfix Expression
3) Reverse a String using Stack
4) Implement two stacks in an array
5) Check for balanced parentheses in an expression

======
Convert Infix to postfix
Infix			Prefix			Postfix
(A+B)*C-D    	-*+ABCD         AB+C*D-
Create stack. For each char check if the char input is operand then just show the operand. If right parentheses comes than pop all the elements until left parenthesis comes out. The values has to be popped according to the priority. If any lower priority comes up than pop the higher priority operator and push lower priority operator.

======
Design stack such that getMinimum should be O(1): Take auxiliary stack that maintains of all values in stack. Whenever something is put into the main stack, if it is minimum after checking in the auxiliary stack, then it is pushed in both the stacks otherwise the same value is pushed into the auxiliary stack. To improve the space complexity we can push in auxiliary stack only when the entered value is the minimum. If the same value is again put in, then it is put in again into the stack
1 
5
1	
4	1
6	1
2	2

======
Palindrome questions can be solved using stacks.

=====
Given an expression, find and mark matched and unmatched parenthesis in it. We need to replace all balanced opening parenthesis with 0, balanced closing parenthesis with 1 and all unbalanced with -1. Input : ((a), Output : -10a1
- We run a loop from the start of the string up to end and for every ‘(‘, we push it into stack. If stack is empty and we encounter an closing bracket ‘)’ the we replace -1 at that index of the string. Else we replace all opening brackets ‘(‘ with 0 and closing brackets with 1. Then pop from the stack.

======
**Given an array of n elements and q queries, for each query which has an index i, find the next greater element and print its value. If there is no such greater element to its right then print -1.
To be done

======
**Sort a stack using a temporary stack. Given a stack of integers, sort it in ascending order using another temporary stack.
Create a temporary stack say tmpStack. While input stack is NOT empty do this: Pop an element from input stack call it temp while temporary stack is NOT empty and top of temporary stack is greater than temp, pop from temporary stack and push it to the input stack. push temp in temporary stack. The sorted numbers are in tmpStack. https://www.geeksforgeeks.org/sort-stack-using-temporary-stack/

======
What is the most appropriate data structure to print elements of queue in reverse order: Stack

======
A stack is an ordered list in which insertion and deletion happens at one end called top. Last element inserted is first element deleted. LIFO. Applications: Balancing of symbol, infix to postfix, evaluation of postfix, implementing function calls, finding of spans, undo sequence in a text editor, page-visited history in web browser (back button), matching tags in HTML and XML

======
We can evaluate infix expression using 2 stacks in 1 go. One stack for operators and one stack for operand.

======
Checking of symbols
Stack<Character> stack = new Stack();
	String str = "()(()[()])";
	for (int i = 0; i < str.length(); i++) {
	    if (str.charAt(i) == '(' || str.charAt(i) == '[') {
	        stack.push(str.charAt(i));
	    } else {
	        if (!stack.isEmpty()) {
	            if (str.charAt(i) == ']' && stack.pop().charValue() != '[') {
	                System.out.println("Symbols are not matching");
	                break;
	            } else if (str.charAt(i) == ')' && stack.pop().charValue() != '(') {
	                System.out.println("Symbols are not matching");
	                break;
	            }
	        } else {
	            System.out.println("Symbols are not matching");
	            break;
	        }
	    }
	}
}

========
Infix to postfix A*B-(C+D)+E   AB*CD+-E+
// driver program to test above functions
public static void main(String[] args) {
    Stack<Character> stack = new Stack();
    String str = "A*B-(C+D)+E";
    for (int i = 0; i < str.length(); i++) {
        if (Character.isLetter(str.charAt(i))) {
            System.out.print(str.charAt(i));
        } else if (str.charAt(i) == '(') {
            stack.push(str.charAt(i));
        } else if (str.charAt(i) == ')') {
            while(stack.peek() != '('){
                System.out.print(stack.pop());
            }
            stack.pop();
        } else {
            while(function(stack.peek()) >= function(str.charAt(i))){
                System.out.print(stack.pop());
            }
            stack.push(str.charAt(i));
        }
    }
}

static int function(char ch){
    switch (ch){
        case '+':
        case '-':
            return 1;

        case '*':
        case '/':
            return 2;

        case '^':
            return 3;
    }
    return -1;
}

======
Finding the spans IN STOCK MARKET. The span of a stock on a certain day i, is maximum number of consecutive days the price of stock has been less or equal to its price on i
Stack stack = Stack()
int p=0
for (int i=0; i<inputArr.length; i++){
	while(!isEmpty() && inputArray[i] > inputArray[stack.top()]){
		stack.pop()
	}
	if(stack.isEmpty()){
		p = -1
	}else{
 		p = stack.top()
	}
	spans[i] = i - p
	stack.push(i)
}

======
How to implement a stack using queue? A stack can be implemented using two queues. Let stack to be implemented be ‘s’ and queues used to implement be ‘q1’ and ‘q2’. Stack ‘s’ can be implemented in two ways:
Method 1 (By making push operation costly)
push
  1) Enqueue x to q2
  2) One by one dequeue everything from q1 and enqueue to q2.
  3) Swap the names of q1 and q2. Swapping of names is done to avoid one more movement of all elements from q2 to q1.
pop
  1) Dequeue an item from q1 and return it.

Method 2 (By making pop operation costly) See Implement Stack using Queues
 push(s, x)
  1) Enqueue x to q1 (assuming size of q1 is unlimited).

pop(s)  
  1) One by one dequeue everything except the last element from q1 and enqueue to q2.
  2) Dequeue the last item of q1, the dequeued item is result, store it.
  3) Swap the names of q1 and q2
  4) Return the item stored in step 2. Swapping of names is done to avoid one more movement of all elements from q2 to q1.

==========
QUEUE
==========
QUEUE: Queue is a linear structure which follows the order is First In First Out (FIFO) to access elements. Mainly the following are basic operations on queue: Enqueue, Dequeue, Front, Rear. The difference between stacks and queues is in removing. In a stack we remove the item the most recently added; in a queue, we remove the item the least recently added. Both Queues and Stacks can be implemented using Arrays and Linked Lists. Operating system job scheduling in order of arrival. Multiprogramming. Waiting times of customers at call center. If making the queue using array, it is best to use the circular array.

=====
Deque also known as double ended queue, as name suggests is a special kind of queue in which insertions and deletions can be done at the last as well as at the beginning

=====
How to implement a queue using stack? A queue can be implemented using two stacks. Let queue to be implemented be q and stacks used to implement q be stack1 and stack2. q can be implemented in two ways:
Method 1 (By making enQueue operation costly)
Method 2 (By making deQueue operation costly) See Implement Queue using Stacks
