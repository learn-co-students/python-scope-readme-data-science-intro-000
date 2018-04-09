
# Working with Scope

### Learning Objectives

* Understand global variables in Python
* Understand local variables in Python and why they are a good feature of Python

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


Somehow, our `words` variable is suddenly inaccessible. Python has various rules about when and how to access variables and data throughout a file. As we'll see in this lesson, accessibility of a variable depends on whether that variable is a global variable or a local variable. We will also see how a function's return statement allows us to send data inside of a function into global scope. 

### Global variables

Before our introuction to functions in the recent lesson, we always had access to any variable we had declared in Python.


```python
number = 1
```


```python
number
```

We weren't thinking about it, but we were operating in the global scope. Whenever we declare a variable that is not declared inside of a function, we are operating in global scope. This means that the variable is available anywhere in current file.

  Accordingly, we can access the variable from outside of a function...


```python
number
```

...or inside of a function.


```python
def access_to_globals():
    # we can access global variables from inside of our function
    return number

access_to_globals()
```

Global variables are a priviledged bunch.  Once declared, they can be referenced either inside or outside of a function.  

### Local variables

Local variables are resigned to a different fate than global variables.  Below, the variable `trapped` is a local variable.


```python
def locals_stay_local():
    trapped = 'not escaping'
```


```python
locals_stay_local()
```

Unlike our global variable `number`, `trapped` is first declared from inside a function, making it a local variable. 


```python
trapped
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-4-956155b55e40> in <module>()
    ----> 1 trapped
    

    NameError: name 'trapped' is not defined


Because the variable `trapped` is declared inside a function, it can only be referenced from that function. Believe it or not, this is a helpful feature. By declaring a local variable, we know that we only have to pay attention to that variable from inside the body of the function. We do not have to search our file to see what that variable may have been assigned or reassigned to.

And from inside of the function, we can use that variable to make our code more expressive.


```python
def no_return_full_name():
    first_name = 'bob'
    last_name = 'smith'
    full_name = first_name + ' ' + last_name
```

### Return statements

Of course we want our function to have some impact outside of itself.  To do that, we use a `return` statement.

Let's execute our function `no_return_full_name`.


```python
no_return_full_name()
```


```python
full_name
```

If you press shift + enter on the two code blocks above, you have executed our function and then tried to reference the variable `full_name`. However, because the variable `full_name` is local, it is only available from inside of the function.  That's not very useful.  

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



Now the string `'bob smith'` is returned from the function.  Notice that the `full_name` is still not available globally.


```python
full_name
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-5-1ef4381f016d> in <module>()
    ----> 1 full_name
    

    NameError: name 'full_name' is not defined


However, we did throw the variable's value over the wall, and if we wish to use it with more code we can.  For example, we can combine the return value with another expression:


```python
'Hello ' + return_full_name()
```

Or we can assign the return value to a global variable, and access it from that variable.


```python
a_fine_name = return_full_name()
a_fine_name
```




    'bob smith'



So variables declared inside of a function are still only available locally.  However, by using a return statement we can throw the data over the wall of the function and into global scope.  

Another thing to note about a return statement is that once a function reaches the return statement, no other lines of the function are executed.


```python
def return_statements():
    print("this is executed")
    return "this is the function's output"
    print("this is not executed")
return_statements()
```

    this is executed





    "this is the function's output"



So, return statements are an important feature of functions as they terminate the execution of a function and throw the result of the function into global scope.

### Summary

In this section we learned about scope. We saw how when we declare a variable outside of a function, we are declaring that variable in global scope. This means that the variable is available throughout the file it is declared in - inside and outside of functions. Variables declared inside of functions are local variables and are available to be referenced from inside of the function in which they are declared. However, we can access the local variable outside of the function by using the `return` keyword at the end of our function. The combination of local variables and returning specific data allows us to encapsulate our code inside of a function and explicitly state what should be returned, and thus accessible from outside of the function.
