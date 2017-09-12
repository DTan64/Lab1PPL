# Lab 1
## Title: Lab 1 Writeup for Questions
## Team: Juan Vargas-Murillo and D'Artagnan Wake

2. <b>Scala Basics: Binding and Scope</b>. For each the following uses of names, give the
line where that name is bould. Briefly explain your reasoning (in no more than 1-2 sentences).

   (a) Consider the following Scala code.
   
      ```scala
      1     val pi = 3.14
      2     def circumference(r: Double): Double = {
      3        val pi = 3.14159
      4        2.0 * pi * r
      5     }
      6     def area(r: Double): Double =
      7        pi * r * r
      ```
     The use of *pi* at line 4 is bound at which line? The use of *pi* at line 7
     is bound at which line?
     
     **Answer**: 
    
      -The use of *pi* at line 4 is bound at line 3 where the declaration of val pi = 3.14159 happens.
     It is bound at line 3 also because we have introduced curly braces on lines 2 and 5 which create a new scope level.
     
      -The use of *pi* at line 7 is bound line 1 where the delcaration of val pi = 3.14 happens.
      It is also a part of the global scope.
     
     (b) Consider the following Scala code.
     
      ```scala
      1     val x = 3
      2     def f(x: Int): Int =
      3        x match {
      4           case 0 => 0
      5           case x => {
      6              val y = x + 1
      7              ({
      8                 val x = y + 1
      9                 y
      10              } * f(x - 1)
      11          }
      12       }
      13    val y = x + f(x)
      ```
      The use of *x* at line 3 is bound at which line? The use of *x* at line 6 is bound at which
      line? The use *x* at line 10 is bound at which line? The use of *x* at line 13 is bound at
      which line?
      
      **Answer**:
      
      -The use of *x* at line 3 is bound at line 2 where *x* is passed into the function and where
      it is also being declared as type Int. 
      
      -The use of *x* at line 6 is bound at line 5 because it is in the scope of the match when it is case x.
      The x for case x is a placeholder.
      
      -The use of *x* at line 10 is bound at line 5 because it falls within the scope when the match is case x
      Same as *x* at line 6.
      
      -The use of *x* at line 13 is bound at line 1 since it is in the global scope. 
    
    
3. <b>Scala Basics: Typing.</b> In the following, I have left off the return type of function g. The body
of g is well-typed if we can come up with a valid return type. Is the body of g well-typed?

      ```scala
      1     def g(x: Int) = {
      2        val (a, b) = (1, (x, 3))
      3        if (x == 0) (b, 1) else (b, a + 2)
      4     }
      ```
      
   If so, give the return type of g and explain how you determined this type. For this explanation,
   first, give the types for the names a and b. Then, explain the body expression using the following format:
   
   ```
      
      e:τ because
      
         e1:τ1
      
            ...
      
         e2:τ2 because
      
            ...
   ```
   where *e1* and *e2* are subexpressions of *e*. Stop when you reach values (or names).
   As an example of the suggested format, consider the plus function:
   ```scala
   def plus(x: Int, y: Int) = x + y
   ```
   
   Yes, the body of the expression of plus is well-typed with type Int.
   
   ```
   x + y: Int because
      x: Int
      y: Int
   ```
   
   **Answer**:
   
   The function g is well-typed and should have the return type of a tuple of a tuple of ints and an int.(i.e)
   ```scala
   1     def g(x: Int): Tuple((Int, Int), Int) = {
   2        val (a, b) = (1, (x, 3))
   3        if (x == 0) (b, 1) else (b, a + 2)
   4     }
   ```
   
   **g:( (Int, Int), Int) because
   ```
   If True  (b, 1): ( (Int, Int), Int) because
      
               b: (Int, Int) because            
                  (x, 3): (Int, Int) because               
                       x: Int                 
                       3: Int          
                1: Int
          
   Else     (b, a + 2): ( (Int, Int), Int) because            
               b: (Int, Int) because            
                  (x, 3): (Int, Int) because               
                       x: Int                 
                       3: Int                 
              a + 2: Int because            
               a: Int
               2: Int
   ```
   
   
