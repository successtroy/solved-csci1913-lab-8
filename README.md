Download Link: https://assignmentchef.com/product/solved-csci1913-lab-8
<br>
In this assignment you will implement a stack as a Java class, using a linked list of nodes. Unlike the stack discussed in the lectures, however, your stack will be designed to efficiently handle repeated pushes of the same element. This shows that there are often many different ways to design the same data structure, and that a data structure should be designed for an anticipated pattern of use.

<ol>

 <li></li>

</ol>

The most obvious way to represent a sequence of objects is simply to list them, one after the other, like this.

<em>a</em>  <em>a</em>  <em>b</em>  <em>b</em>  <em>b</em>  <em>c</em>  <em>a</em>  <em>a</em>  <em>d</em>  <em>d</em>  <em>d</em>  <em>d</em>

Note that the same objects often appear many times in a row. This is called a <em>run</em> of those objects. In the example sequence, there is a run of 2 <em>a</em>’s, a run of 3 <em>b</em>’s, a run of 1 <em>c</em>, a run of 2 <em>a</em>’s, and a run of 4 <em>d</em>’s. You can represent a sequence with runs by listing its objects, along with the number of times each object appears. For example, you can represent the sequence shown above like this.

<em>a</em>  <em>b</em>  <em>c</em>  <em>a</em>  <em>d</em>

2 3 1 2 4

Representing a sequence in this way is called <em>run-length encoding.</em> If a sequence has long runs, or many runs, then run-length encoding will represent it more efficiently than simply listing its objects. However, if a sequence has short runs, or few runs, then run-length encoding may represent it <em>less</em> efficiently, because extra space is needed to store the lengths of the runs.

Since a stack is just a simple kind of sequence, you can use run-length encoding to implement it. In this assignment, you will write a Java class called RunnyStack that implements a stack which uses run-length encoding. Here are some examples of how it works. Suppose you push an object <em>a</em> on an empty RunnyStack. Then the stack will look like this, with a run of 1 <em>a</em>.

<ul>

 <li>1</li>

</ul>

Now suppose you push <em>b</em>. The stack now looks like this, with a run of 1 <em>b</em>, and a run of 1 <em>a.</em>

<ul>

 <li>1</li>

 <li>1</li>

</ul>

If you push another <em>b</em> on the RunnyStack, then the length of the run on top of the stack is incremented, so the stack looks like this.

<ul>

 <li>2</li>

 <li>1</li>

</ul>

If you push yet another <em>b</em>, then the length of the run at the top of the stack would increase to 3. However, suppose that you pop the RunnyStack instead. Then the length of the run at the top is decremented, so that the stack looks like this.

<ul>

 <li>1</li>

</ul>

<em>a</em> 1

If you pop the RunnyStack one more time, then the length of the run on top of the stack is decremented to 0. However, a run of 0 objects is like no run at all, so it vanishes, and the stack looks as it did after the first push.

<em>a</em> 1

Stacks with run-length encoding are used internally by some compilers and interpreters, because they often push the same objects over and over again.

<ol>

 <li></li>

</ol>

You must write a class called RunnyStack that represents a stack. Your class must implement run-length encoding, as described previously. It must also hold objects of type Base, so it will look like this.

class RunnyStack&lt;Base&gt;

{

⋮

}

Your class must define at least the following methods, as described below. To simplify grading, your methods must have the same names as the ones shown here. public RunnyStack()

Constructor. Make a new, empty instance of RunnyStack. public int depth()

Return the depth of the stack: the sum of the lengths of all the runs it holds. This is not necessarily the same as the number of runs it holds, which is returned by the method runs. public boolean isEmpty()

Test if the stack is empty.

public Base peek()

If the stack is empty, then throw an IllegalStateException. Otherwise, return the Base at the top of the stack. public void pop()

If the stack is empty, then throw an IllegalStateException. Otherwise, decrement the length of the run on top of the stack. If this leaves a run of zero Base’s on top of the stack, then remove that run. public void push(Base base)

If the stack is empty, then add a new run of one Base at the top of the stack. If the stack is not empty, then test if base is equal to the object in the run at the top of the stack. If it is, then increment the length of that run. If it isn’t, then add a new run of one base at the top of the stack. Note that base may be null. public int runs()

Return the number of runs in the stack. This is not necessarily the same as its depth, which is returned by the method depth.

Here are some hints, requirements, and warnings. First, all these methods must work using <em>O</em>(1) operations, so they are not allowed to use loops or recursions. <em>You will receive no points for this assignment if you use loops or recursions in any way!</em>

Second, your RunnyStack class must have a private nested class called Run. You must use instances of Run to implement your stack. Each instance of Run represents a run of Base’s. <em>You will receive no points for this assignment if you use arrays in any way!</em> The class Run must have three private slots that have the following names and types. The slot base points to the Base that appears in the run. The slot length is an int that is the length of the run. The slot next points to the instance of Run that is immediately below this one on the stack, or to null. It must also have a private constructor that initializes these slots.

Third, your push method must test non-null Base’s for equality using their equals methods. It must use the Java ‘==’ operator only for testing null Base’s. It is helpful to define an extra private method called isEqual that takes two Base’s as arguments, and tests if they are equal. If either Base is null, then isEqual uses ‘==’. If neither Base is null, then isEqual uses equals.

Fourth, RunnyStack’s methods are not allowed to print things. If you were writing RunnyStack in the Real World, then it might be part of some larger program. You don’t know if that larger program should print things.