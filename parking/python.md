## Memorize

```
def memoize(func):
    cache = {}
    def wrapper(*args):
        if args in cache:
            return cache[args]
        else:
            result = func(*args)
            cache[args] = result
            return result
    return wrapper
```

The decorator uses a dictionary, stores the function args, and returns values. When we execute this function, the decorated will check the dictionary for prior results. The actual function is called only when there’s no stored value before.

The following is a Fibonacci number calculating a function. Since this is a recurrent function, the same function called is performed multiple times. But with caching, we can speed up this process.
```
@memoize
def fibonacci(n):
    if n <= 1:
        return n
    else:
        return fibonacci(n-1) + fibonacci(n-2)
```


## Timing

```
import time

def timing_decorator(func):
    def wrapper(*args, **kwargs):
        start_time = time.time()
        result = func(*args, **kwargs)
        end_time = time.time()
        print(f"Function {func.__name__} took {end_time - start_time} seconds to run.")
        return result
    return wrapper
```

You can use this decorator to time the execution of a function:

```
@timing_decorator
def my_function():
    # some code here
    time.sleep(1)  # simulate some time-consuming operation
    return
```