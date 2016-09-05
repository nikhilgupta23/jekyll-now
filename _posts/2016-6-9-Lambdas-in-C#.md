---
layout: post
title: Lambdas in C#
---
Recently, I got a chance to experiment with __Lambda expressions__ in C#. _It was love at first sight_ :P

A lambda expression is an anonymous function that you can use to create delegates or expression tree types. 
By using lambda expressions, you can write local functions that can be passed as arguments or returned as the value of function calls.
Lambda expressions are particularly helpful for writing LINQ query expressions.

As an example- _Find the square of a number._

A normal course of action will be-
1. Create a delegate.
2. Create a function of that delegate type.
3. Make the call.

```C#
delegate int del(int i);
static int SquareOfNum(int num)
{
    return num*num;
}
static void Main(string[] args)
{
    del myDelegate = new del(SquareOfNum);
    int j = myDelegate(5); //j = 25
}
```
Anonymous methods make the code shorter and allow the usage of functions without giving them any names.

```C#
delegate int del(int i);
public static void Main(string[] args)
{
    del myDelegate = delegate(int num)
    {
      return num*num;
    };
    int j = myDelegate(5); //j = 25
}
```
Lambdas take it a step further-
```C#
delegate int del(int i);
public static void Main(string[] args)
{
    del myDelegate = x => x * x;
    int j = myDelegate(5); //j = 25
}
```
Notice that the data type of _x_ was not provided. It is inferred directly from the delegate _del_.
Also, the keyword _return_ is not used in the above example. 
If the function has multiple statements, a body can be created with a _return_ statement.
```C#
delegate int del(int i);
public static void Main(string[] args)
{
    del myDelegate = x => 
    {
      return x * x;
    };  
    int j = myDelegate(5); //j = 25
}
```

This example is really silly but it helps in understanding the basics. 
Lambdas can prove to be really powerful when used with event-driven programming and with LINQ.
They make the code shorter and easy to understand.
