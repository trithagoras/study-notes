# Chapter 1: Lambda Calculus

## 1.2. What is functional programming?

> Functional programming is a paradigm that relies on functions modeled on mathematical functions.

* Programs are a series of *expressions*
* Expressions include concrete values, variables, and functions.

> Functions are expressions that are applied to an argument, and once applied, can be *reduced* or *evaluated*.

Functional programming languages are all based on the lambda calculus. Haskell is a *pure* functional language, meaning it adheres to *referential transparency*.

**Referential transparency** means that the same function applied to the same arguments will produce the same output. Always. They resemble pure functions in math.


## 1.4. The structure of lambda terms

The lambda calculus has three basic components: **expressions, variables,** and **abstractions**.
* Variables have no meaning or value, they are just names for potential inputs to functions (parameters).
* Arguments are input values
* Abstractions are functions. It has a *head* and a *body*, where the head is a lambda λ followed by a variable name, and a body is another expression.


The variable named in the head of an abstraction is a *parameter* and *binds* all instances of that same variable in the body of the function.

> Basic lambda calculus has that lambda functions are all anonymous (unnamed).

Given the simple abstraction:
$$\lambda x.x$$

The $\lambda x.$ is the head of the abstraction, and the final $x$ is the body. Specifically in this case, it is a bound variable.


### Alpha equivalence

Given the previous $\lambda x.x$, we note that the name of the parameter $x$ is not meaningful, and that $\lambda z.z$ is **completely equivalent**.


## 1.5. Beta reduction

When applying a function to an argument, we substitute the value for all instances of bound variables in the body. You also eliminate the head of the abstraction. This process is called **beta reduction**.

Consider the previous function once more:

$$\lambda x.x$$

We can apply the function to the number 2:

$$(\lambda x.x) 2\\
2$$

Note that this function which takes an argument and returns the unchanged argument is the **identity function** (and indeed, is the unnamed equivalent to the mathematical identity function, $f(x) = x$).

We can also apply our identity function to another lambda abstraction:

$$(\lambda x.x)(\lambda y.y)$$

(Recall that these two functions are equivalent, even though their parameters are different.)

We can use a new syntax here $[x \coloneqq (\lambda y.y)]$, to indicate that $(\lambda y.y)$ will be substituted for all instances of $x$. We reduce this application like this:

$$
(\lambda x.x)(\lambda y.y)\\
[x \coloneqq (\lambda y.y)]\\
\lambda y.y
$$

The final result is another identity function, and there are no arguments to apply the function to, so this expression is fully reduced.

Let's do the same example now, but introduce another argument:

$$(\lambda x.x)(\lambda y.y)z$$

Applications in the lambda calculus are *left associative*, meaning they associate to the left. In other words, the previous function is implicitly equal to:

$$((\lambda x.x)(\lambda y.y))z$$

Which can be reduced to:

$$
(\lambda x.x)(\lambda y.y)z\\
[x \coloneqq (\lambda y.y)]\\
(\lambda y.y)z\\
[y \coloneqq z]\\
z
$$

This expression is now fully reduced, and the computation is complete. Again, to summarise, beta reduction of an abstraction is simply the process of replacing the bound variables with the value of the argument and eliminating the head.

Note that $z$ is meaningless here. In fact, it is known as a *free variable*.

### Free variables

Given:

$$\lambda x.xy$$

$y$ is a free variable, and $x$ is a bound variable. When applying this function to an argument, nothing can be done with the $y$. It is unreducible.

Note: alpha equivalence does not apply to free variables. i.e.

$$
\lambda x.xy \not\equiv \lambda x.xz
$$

because $y$ and $z$ may be different.


## Summary:

