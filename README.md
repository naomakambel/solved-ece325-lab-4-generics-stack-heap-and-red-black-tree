Download Link: https://assignmentchef.com/product/solved-ece325-lab-4-generics-stack-heap-and-red-black-tree
<br>
Generics, or parameterized types, are a facility of generic programming that was added to the Java programming language in 2004 as part of Java 5 (JDK 1.5). They allow “a type or method to operate on objects of various types while providing compile-time type safety”. A common usage of this feature is when using a Java <em>Collection</em> that can hold objects of any type, to specify the specific type of object stored in it. In this lab, we try to address Generics for containers, such as vectors and stacks.

A Java collection (we will explore more in Lab 5) is a flexible data structure that can hold heterogeneous objects where the elements may have any reference type. It is your responsibility, however, to keep track of what types of objects your collections contain. For example, consider adding an integer to a collection:

<table width="48">

 <tbody>

  <tr>

   <td width="48">Integer</td>

  </tr>

 </tbody>

</table>

since you cannot have collections of primitive data types you must convert it to the corresponding reference type (i.e. ) before storing it in the collection.

The motivation for adding generics to the Java programming language stems from the lack of information about a collection’s element type, the need for developers to keep track of what type of elements collections contain, and the need for casts all over the place. Using generics, a collection is no longer treated as a list of object references, but you would be able to differentiate between a collection of references to integers and collection of references to bytes. A collection with a generic type has a type parameter that specifies the element type to be stored in the collection. So, instead of relying on the programmer to keep track of object types and performing casts, which could lead to failures at <strong>runtime</strong>, the compiler can now help the programmer enforce a greater number of type checks and detect more failures at compile time.

This is a quick example of this application of Generics in the casting problem.

List<strong>&lt;</strong>Apple<strong>&gt;</strong> box<strong>;</strong>

<em>// Put some apples in the box</em>

Apple apple <strong>=</strong> box<strong>.</strong>get<strong>(</strong>0<strong>);</strong>

The main advantage of generics is having the compiler keep track of type parameters, perform the type checks and the casting operations. The compiler guarantees that the casts will never fail.

<h2>1.2  The Generic Facility</h2>

The generics facility introduced the concept of type variable. A type variable, according to the Java language specification, is an unqualified identifier introduced by:

<ul>

 <li>Generic class declarations</li>

 <li>Generic interface declarations</li>

 <li>Generic method declarations</li>

 <li>Generic constructor declarations</li>

</ul>

Moreover, other Java concepts can be used in a generic manner:

<ul>

 <li>A <strong>class</strong> is generic if it declares <em>one or more</em> type variables. These type variables are known as the type parameters of the class. All of these parameterized types share the same class at runtime:</li>

</ul>

<strong>public</strong> <strong>class</strong> <strong>Foo</strong><strong>&lt;</strong>T<strong>&gt;</strong> <strong>{</strong> <strong>}</strong>

<ul>

 <li>An <strong>interface</strong> is generic if it declares <strong>one or more</strong> type variables. These type variables are known as the type parameters of the interface. Similar to the above, all parameterized types share the same interface at runtime:</li>

</ul>

<strong>public</strong> <strong>interface</strong> <strong>Foo</strong><strong>&lt;</strong>T<strong>&gt;</strong> <strong>{</strong> <strong>}</strong>

<ul>

 <li>A <strong>method</strong> is generic if it declares <strong>one or more</strong> type variables. These type variables are known as the formal type parameters of the method. The formal type parameter list is identical to a type parameter list of a class or interface:</li>

</ul>

<strong>public</strong> <strong>&lt;</strong>T<strong>&gt;</strong> T <strong>getT</strong><strong>()</strong> <strong>{</strong> <strong>}</strong>

<ul>

 <li>A <strong>constructor</strong> can be declared as generic, independently of whether the class itself is generic or not. A constructor is generic if it declares <strong>one or more</strong> type variables. These type variables are known as the formal type parameters of the constructor. The formal type parameter list is identical to a type parameter list of a generic class or interface:</li>

</ul>

<strong>public</strong> <strong>class</strong> <strong>Foo</strong><strong>&lt;</strong>T<strong>&gt;</strong> <strong>{</strong>     <strong>public</strong> <strong>&lt;</strong>E<strong>&gt;</strong> <strong>Foo</strong><strong>(</strong>E e<strong>)</strong> <strong>{</strong> <strong>}</strong>

<strong>}</strong>

<strong>new</strong> Foo<strong>&lt;</strong>Integer<strong>&gt;(</strong>“I’m a string”<strong>);</strong>

<h2>1.3  Bounded Types</h2>

<table width="41">

 <tbody>

  <tr>

   <td width="41">Number</td>

  </tr>

 </tbody>

</table>

There may be times when you want to restrict the types of the generics. For example, a method that operates on numbers might only want to accept instances of  or its subclasses. This is what

<table width="669">

 <tbody>

  <tr>

   <td colspan="5" width="669">bounded type parameters are for. To declare a bounded type parameter, list the type parameter’s name,</td>

  </tr>

  <tr>

   <td width="100">followed by the</td>

   <td width="48">extends</td>

   <td width="462"> keyword, and then followed by its <em>upper bound</em>, which, in this example, is</td>

   <td width="41">Number</td>

   <td width="17">.</td>

  </tr>

  <tr>

   <td colspan="5" width="669">Note that in this context, extending is used in a general sense to mean either “extends” (as in classes) or</td>

  </tr>

 </tbody>

</table>

“implements” (as in interfaces).

<strong>&lt;</strong>T <strong>extends</strong> SomeSuperClassOrInterface<strong>&gt;</strong>

<h1>2  Stack</h1>

The stack represents a <em>last-in-first-out</em> (LIFO) list of objects. It extends vector with five operations that allow a vector to be treated as a stack:

<table width="28">

 <tbody>

  <tr>

   <td width="28">peek</td>

  </tr>

 </tbody>

</table>

<ul>

 <li>: query the top element of the stack. <strong>The top element is the only accessible element</strong>. If the stack is empty, then you can peek nothing.</li>

 <li><sub>push</sub>: add a new element to the top of the stack. If the stack has a max size and is full, then you cannot successfully push.</li>

 <li><sub>pop</sub>: remove the top element of the stack. If the stack is already empty, then you cannot successfully pop.</li>

 <li>size: query the size of the stack.</li>

 <li>isEmpty: query if the stack is empty or not.</li>

</ul>

<h1>3  Postfix Expression</h1>

<table width="35">

 <tbody>

  <tr>

   <td width="35">1 2 +</td>

  </tr>

 </tbody>

</table>

Postfix notation, also known as <em>reverse Polish notation</em>, is a syntax for mathematical expressions where the mathematical operator is always placed after the operands. For instance, the addition of 1 and 2 would be written in postfix notation as . Computer scientists and software developers are interested in postfix notation because it can be easily and efficiently evaluated with a simple stack machine. Moreover, postfix notation has been used in some hand-held calculators because it enables arbitrarily complex expressions to be entered and evaluated without the use of parentheses and without requiring the user to keep track of intermediate results.

Here are some simple postfix expressions and their results.

<strong>Postfix Expression                                                                 Result </strong>

<strong>Postfix Expression                                                                 Result </strong>

9

8

<h1>4  Deliverable 1 — Postfix Expression Calculator by Generic Stack</h1>

<em>Step 1: </em>

Refer to the <em>GenericStack.java</em>, and finish the five methods of stack operations.

<em>Step 2: </em>

<table width="140">

 <tbody>

  <tr>

   <td width="140">calcPostfixExpression</td>

  </tr>

 </tbody>

</table>

Finish the  method following the brief algorithm:

<ul>

 <li>Initialize the stack.</li>

 <li>Parse the expression string into an array of symbols, and feed them to the stack one by one.</li>

 <li>If the next symbol is an operand (numbers), then push it to the stack.</li>

 <li>If the next symbol is an operator, then there must be at least two operands already in the stack. Pop the two operands to do the corresponding calculation, and then re-push the result back to the stack.</li>

 <li>Repeat through all the symbols.</li>

 <li>Finally, we have only one element in the stack — it is the final result. Pop and print it out.</li>

</ul>

<strong>DEMO this deliverable to the lab instructor (10 points).</strong>

<h1>5  Deliverable 2 — Generic Heap</h1>

Make your heap sort algorithm generic. Please refer to the <em>GenericHeap.java</em>, and finish the TODO codes.

<strong>DEMO this deliverable to the lab instructor (5 points).</strong>

<h1>6  Deliverable 3 — Generic Red Black Tree</h1>

Make your red black tree algorithm generic. Please refer to the <em>GenericRedBlackTree.java</em>, and finish the

<table width="669">

 <tbody>

  <tr>

   <td width="277">TODO codes. Note you need also finish the</td>

   <td width="41">delete</td>

   <td width="350"> method.</td>

  </tr>

 </tbody>

</table>