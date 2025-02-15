# Automatic differentiation with `autograd`
:label:`crash_course_autograd`

We train models to get better and better as a function of experience. Usually, getting better means minimizing a loss function. To achieve this goal, we often iteratively compute the gradient of the loss with respect to weights and then update the weights accordingly. While the gradient calculations are straightforward through a chain rule, for complex models, working it out by hand can be a pain.

Before diving deep into the model training, let's go through how MXNet’s `autograd` package expedites this work by automatically calculating derivatives.

## Basic usage

Let's first import the `autograd` package.

```{.python .input}
from mxnet import np, npx
from mxnet import autograd
npx.set_np()
```

As a toy example, let’s say that we are interested in differentiating a function $f(x) = 2 x^2$ with respect to parameter $x$. We can start by assigning an initial value of $x$.

```{.python .input  n=3}
x = np.array([[1, 2], [3, 4]])
x
```

Once we compute the gradient of $f(x)$ with respect to $x$, we’ll need a place to store it. In MXNet, we can tell an ndarray that we plan to store a gradient by invoking its `attach_grad` method.

```{.python .input  n=6}
x.attach_grad()
```

Now we’re going to define the function $y=f(x)$. To let MXNet store $y$, so that we can compute gradients later, we need to put the definition inside a `autograd.record()` scope.

```{.python .input  n=7}
with autograd.record():
    y = 2 * x * x
```

Let’s invoke back propagation (backprop) by calling `y.backward()`. When $y$ has more than one entry, `y.backward()` is equivalent to `y.sum().backward()`.
<!-- I'm not sure what this second part really means. I don't have enough context. TMI?-->

```{.python .input  n=8}
y.backward()
```

Now, let’s see if this is the expected output. Note that $y=2x^2$ and $\frac{dy}{dx} = 4x$, which should be `[[4, 8],[12, 16]]`. Let's check the automatically computed results:

```{.python .input  n=9}
x.grad
```

## Using Python control flows

Sometimes we want to write dynamic programs where the execution depends on some real-time values. MXNet will record the execution trace and compute the gradient as well.

Consider the following function `f`: it doubles the inputs until it's `norm` reaches 1000. Then it selects one element depending on the sum of its elements.
<!-- I wonder if there could be another less "mathy" demo of this -->

```{.python .input}
def f(a):
    b = a * 2
    while np.abs(b).sum() < 1000:
        b = b * 2
    if b.sum() >= 0:
        c = b[0]
    else:
        c = b[1]
    return c
```

We record the trace and feed in a random value:

```{.python .input}
a = np.random.uniform(size=2)
a.attach_grad()
with autograd.record():
    c = f(a)
c.backward()
```

We know that `b` is a linear function of `a`, and `c` is chosen from `b`. Then the gradient with respect to `a` be will be either `[c/a[0], 0]` or `[0, c/a[1]]`, depending on which element from `b` we picked. Let's find the results:

```{.python .input}
a.grad == c/a
```

## Next Steps

Now we can train a neural network now: :ref:`crash_course_train`.
