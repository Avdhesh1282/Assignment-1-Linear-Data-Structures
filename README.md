# Assignment-1-Linear-Data-Structures
Problem for Assignment-2: Linear Data Structures


#1-----------Delete the elements in an linked list whose sum is equal to zero
# A Linked List Node
class ListNode:
    def __init__(self, val):
        self.val = val
        self.next = None
 
# Function to create Node
def getNode(data):
    temp = ListNode(data)
    temp.next = None
    return temp
 
# Function to print the Linked List
def printList(head):
    while (head.next):
        print(head.val, end=' -> ')
        head = head.next
    print(head.val, end='')
 
# Function that removes continuous nodes
# whose sum is K
def removeZeroSum(head, K):
 
    # Root node initialise to 0
    root = ListNode(0)
 
    # Append at the front of the given
    # Linked List
    root.next = head
 
    # Map to store the sum and reference
    # of the Node
    umap = dict()
 
    umap[0] = root
 
    # To store the sum while traversing
    sum = 0
 
    # Traversing the Linked List
    while (head != None):
 
        # Find sum
        sum += head.val
 
        # If found value with (sum - K)
        if ((sum - K) in umap):
 
            prev = umap[sum - K]
            start = prev
 
            # Delete all the node
            # traverse till current node
            aux = sum
 
            # Update sum
            sum = sum - K
 
            # Traverse till current head
            while (prev != head):
                prev = prev.next
                aux += prev.val
                if (prev != head):
                    umap.remove(aux)
 
            # Update the start value to
            # the next value of current head
            start.next = head.next
 
        # If (sum - K) value not found
        else:
            umap[sum] = head
 
        head = head.next
 
    # Return the value of updated
    # head node
    return root.next
 
 
# Driver Code
if __name__ == '__main__':
 
    # Create Linked List
    head = getNode(1)
    head.next = getNode(2)
    head.next.next = getNode(-3)
    head.next.next.next = getNode(3)
    head.next.next.next.next = getNode(1)
 
    # Given sum K
    K = 5
 
    # Function call to get head node
    # of the updated Linked List
    head = removeZeroSum(head, K)
 
    # Print the updated Linked List
    if(head != None):
        printList(head)
        
        
        
   #2----------Reverse a linked list in groups of given size
     
class Node:
  
    # Constructor to initialize the node object
    def __init__(self, data):
        self.data = data
        self.next = None
  
  
class LinkedList:
  
    # Function to initialize head
    def __init__(self):
        self.head = None
  
    def reverse(self, head, k):
        
        if head == None:
          return None
        current = head
        next = None
        prev = None
        count = 0
  
        # Reverse first k nodes of the linked list
        while(current is not None and count < k):
            next = current.next
            current.next = prev
            prev = current
            current = next
            count += 1
  
        # next is now a pointer to (k+1)th node
        # recursively call for the list starting
        # from current. And make rest of the list as
        # next of first node
        if next is not None:
            head.next = self.reverse(next, k)
  
        # prev is new head of the input list
        return prev
  
    # Function to insert a new node at the beginning
    def push(self, new_data):
        new_node = Node(new_data)
        new_node.next = self.head
        self.head = new_node
  
    # Utility function to print the linked LinkedList
    def printList(self):
        temp = self.head
        while(temp):
            print(temp.data,end=' ')
            temp = temp.next
  
  
# Driver program
llist = LinkedList()
llist.push(9)
llist.push(8)
llist.push(7)
llist.push(6)
llist.push(5)
llist.push(4)
llist.push(3)
llist.push(2)
llist.push(1)
  
print("Given linked list")
llist.printList()
llist.head = llist.reverse(llist.head, 3)
  
print ("\nReversed Linked list")
llist.printList()



#3------------Merge a linked list into another linked list at alternate positions.
class Node(object):
    def __init__(self, data:int):
        self.data = data
        self.next = None
  
  
class LinkedList(object):
    def __init__(self):
        self.head = None
          
    def push(self, new_data:int):
        new_node = Node(new_data)
        new_node.next = self.head
        # 4. Move the head to point to new Node
        self.head = new_node
          
    # Function to print linked list from the Head
    def printList(self):
        temp = self.head
        while temp != None:
            print(temp.data)
            temp = temp.next
              
    # Main function that inserts nodes of linked list q into p at alternate positions. 
    # Since head of first list never changes
    # but head of second list/ may change, 
    # we need single pointer for first list and double pointer for second list.
    def merge(self, p, q):
        p_curr = p.head
        q_curr = q.head
  
        # swap their positions until one finishes off
        while p_curr != None and q_curr != None:
  
            # Save next pointers
            p_next = p_curr.next
            q_next = q_curr.next
  
            # make q_curr as next of p_curr
            q_curr.next = p_next  # change next pointer of q_curr
            p_curr.next = q_curr  # change next pointer of p_curr
  
            # update current pointers for next iteration
            p_curr = p_next
            q_curr = q_next
            q.head = q_curr
  
  
  
# Driver program to test above functions
llist1 = LinkedList()
llist2 = LinkedList()
  
# Creating LLs
  
# 1.
llist1.push(3)
llist1.push(2)
llist1.push(1)
llist1.push(0)
  
# 2.
for i in range(8, 3, -1):
    llist2.push(i)
  
print("First Linked List:")
llist1.printList()
  
print("Second Linked List:")
llist2.printList()
  
# Merging the LLs
llist1.merge(p=llist1, q=llist2)
  
print("Modified first linked list:")
llist1.printList()
  
print("Modified second linked list:")
llist2.printList()


#4----------In an array, Count Pairs with given sum
 
def getPairsCount(arr, n, sum):
 
    count = 0  # Initialize result
 
    # Consider all possible pairs
    # and check their sums
    for i in range(0, n):
        for j in range(i + 1, n):
            if arr[i] + arr[j] == sum:
                count += 1
 
    return count
 
 
# Driver function
arr = [1, 5, 7, -1, 5]
n = len(arr)
sum = 6
print("Count of pairs is",
      getPairsCount(arr, n, sum))
      
      
#5---------  Find duplicates in an array
numRay = [0, 4, 3, 2, 7, 8, 2, 3, 1]
arr_size = len(numRay)
for i in range(arr_size):
  
    x = numRay[i] % arr_size
    numRay[x] = numRay[x] + arr_size
  
print("The repeating elements are : ")
for i in range(arr_size):
    if (numRay[i] >= arr_size*2):
        print(i, " ")
  
  
  
  
  #6---------Find the Kth largest and Kth smallest number in an array
  def kthSmallest(arr, N, K):
 
    # Sort the given array
    arr.sort()
 
    # Return k'th element in the
    # sorted array
    return arr[K-1]
 
 
# Driver code
if __name__ == '__main__':
    arr = [12, 3, 5, 7, 19]
    N = len(arr)
    K = 2
 
    # Function call
    print("K'th smallest element is",
          kthSmallest(arr, N, K))
          
          
          
    #7------------Move all the negative elements to one side of the array
    def move(arr):
  arr.sort()
 
# driver code
arr = [ -1, 2, -3, 4, 5, 6, -7, 8, 9 ]
move(arr)
for e in arr:
    print(e , end = " ")
    
    
    
    
    #8-------------Reverse a string using a stack data structure
     
def createStack():
    stack = []
    return stack
 
# Function to determine the size of the stack
 
 
def size(stack):
    return len(stack)
 
# Stack is empty if the size is 0
 
 
def isEmpty(stack):
    if size(stack) == 0:
        return true
 
# Function to add an item to stack .
# It increases size by 1
 
 
def push(stack, item):
    stack.append(item)
 
# Function to remove an item from stack.
# It decreases size by 1
 
 
def pop(stack):
    if isEmpty(stack):
        return
    return stack.pop()
 
# A stack based function to reverse a string
 
 
def reverse(string):
    n = len(string)
 
    # Create a empty stack
    stack = createStack()
 
    # Push all characters of string to stack
    for i in range(0, n, 1):
        push(stack, string[i])
 
    # Making the string empty since all
    # characters are saved in stack
    string = ""
 
    # Pop all characters of string and
    # put them back to string
    for i in range(0, n, 1):
        string += pop(stack)
 
    return string
 
 
# Driver program to test above functions
string = "GeeksQuiz"
string = reverse(string)
print("Reversed string is " + string)




#9-----------Evaluate a postfix expression using stack
class Evaluate:
     
    # Constructor to initialize the class variables
    def __init__(self, capacity):
        self.top = -1
        self.capacity = capacity
        # This array is used a stack
        self.array = []
     
    # check if the stack is empty
    def isEmpty(self):
        return True if self.top == -1 else False
     
    # Return the value of the top of the stack
    def peek(self):
        return self.array[-1]
     
    # Pop the element from the stack
    def pop(self):
        if not self.isEmpty():
            self.top -= 1
            return self.array.pop()
        else:
            return "$"
     
    # Push the element to the stack
    def push(self, op):
        self.top += 1
        self.array.append(op)
 
 
    # The main function that converts given infix expression
    # to postfix expression
    def evaluatePostfix(self, exp):
         
        # Iterate over the expression for conversion
        for i in exp:
             
            # If the scanned character is an operand
            # (number here) push it to the stack
            if i.isdigit():
                self.push(i)
 
            # If the scanned character is an operator,
            # pop two elements from stack and apply it.
            else:
                val1 = self.pop()
                val2 = self.pop()
                self.push(str(eval(val2 + i + val1)))
 
        return int(self.pop())
                 
 
             
# Driver program to test above function
exp = "231*+9-"
obj = Evaluate(len(exp))
print ("postfix evaluation: %d"%(obj.evaluatePostfix(exp)))



#10--------------Implement a queue using the stack data structure
class Queue:
    def __init__(self):
        self.s1 = []
        self.s2 = []
 
    def enQueue(self, x):
         
        # Move all elements from s1 to s2
        while len(self.s1) != 0:
            self.s2.append(self.s1[-1])
            self.s1.pop()
 
        # Push item into self.s1
        self.s1.append(x)
 
        # Push everything back to s1
        while len(self.s2) != 0:
            self.s1.append(self.s2[-1])
            self.s2.pop()
 
    # Dequeue an item from the queue
    def deQueue(self):
         
            # if first stack is empty
        if len(self.s1) == 0:
            print("Q is Empty")
     
        # Return top of self.s1
        x = self.s1[-1]
        self.s1.pop()
        return x
 
# Driver code
if __name__ == '__main__':
    q = Queue()
    q.enQueue(1)
    q.enQueue(2)
    q.enQueue(3)
 
    print(q.deQueue())
    print(q.deQueue())
    print(q.deQueue())
 
