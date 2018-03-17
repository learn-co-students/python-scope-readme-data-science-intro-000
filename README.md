
# Working with Scope

### Introduction

In our introduction to functions, we casually introduced something that is quite odd.  Take a look at the following.


```python
def sample_function(): 
    words = 'function body' 
```


```python
words
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-2-993ed7d20d5f> in <module>()
    ----> 1 words
    

    NameError: name 'words' is not defined


Somehow, our `words` variable is suddenly inaccessible.  Python has various rules about when and how to access variables.  It gets into a topic called **scope**, and we will explore it in this lesson.

### Global variables

Before our discussion of functions, we have always had access to any variable we had declared.


```python
number = 1
```


```python
number
```

We have not thought about it, but we were operating in the global scope.  Whenever we declare a variable that is not declared inside of a function, we are operating in global scope.  This means that the variable is available anywhere in current file.  Accordingly, we can access the variable from outside of a function.



```python
number
```

Or inside of a function.


```python
def access_to_globals():
    # we can access global variables from inside of our function
    return number

access_to_globals()
```

Global variables are a priviledged bunch.  Once declared outside of a function, they can be referenced either inside or outside of a function.  

### Local variables

Local variables are resigned to a different fate than global variables.  The variable `trapped` is a local variable.


```python
def locals_stay_local():
    trapped = 'not escaping'
```


```python
locals_stay_local()
```

It is local as it is first declared from inside fo a function.  Because `trapped` it is local variable, it is inaccessible from outside of the function.


```python
trapped
```

Because the variable `trapped` is declared inside of the function, it can only be referenced from inside that function.  Believe it or not, this is a helpful feature.  By using a local variable, we know that we only have to pay attention to that variable from inside the body of the function.  We do not have to search our file to see what that variable equals.

And from inside of the function, we can use that variable to make our code more expressive, just like always.


```python
def no_return_full_name():
    first_name = 'bob'
    last_name = 'smith'
    full_name = first_name + ' ' + last_name
```

### Return statements

Of course we want our function to have some impact outside of itself.  To do that, we use a `return` statement.

Let's execute our function `full_name`.


```python
no_return_full_name()
```


```python
full_name
```

If you press shift + enter on the two code blocks above, you have executed that function and tried to reference the variable `full_name`. However, because all of the variables are local, they only available from inside of the function, and it seems like nothing happened.  

So let's write another function called `return_full_name` that has a return statement.


```python
def return_full_name():
    first_name = 'bob'
    last_name = 'smith'
    full_name = first_name + ' ' + last_name
    return full_name
```


```python
return_full_name()
```




    'bob smith'



Now the string is returned from the function.  Notice that the `full_name` is still not available globally.


```python
first_and_last
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-14-e9b1eade3919> in <module>()
    ----> 1 first_and_last
    

    NameError: name 'first_and_last' is not defined


However, we did throw the variable's value over the wall.  And if we wish to use it with more code we can.  For example, we can combine the return value with another expression:


```python
'Hello ' + return_full_name()
```

Or we can save it's return globally, by storing that `return` value as a variable in global scope.


```python
a_fine_name = return_full_name()
a_fine_name
```




    'bob smith'



So variables declared inside of a function are still only available globally.  However by using a return statement we can throw the data like a string over the wall of the function and into global scope.  

Another thing to note about a return statement is that once a function reaches the return statement, no other lines of the function are executed.


```python
def return_statements():
    'this is executed'
    return 'what'
    'this is not executed'
return_statements()
```




    'what'



### Summary

In this section we learned about scope.  We saw how when we declare a variable outside of a function, we are declaring that variable in global scope.  This means that the variable is available throughout the file it is declared in - inside of functions and out.  Variables declared inside of functions are local variables, and are available to be referenced from inside of the function in which they are declared.  However, we can have the data that a local variable points to be thrown over the walls of the function by using the `return` keyword.  The combination of local variables with returning specific data allows us to encapsulate our code inside of a function, and be explicitly state what should be returned, and thus accessible from outside of the function.
