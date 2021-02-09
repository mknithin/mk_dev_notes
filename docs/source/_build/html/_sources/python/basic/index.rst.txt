######################
Python language basics
######################

Apple mac book pro is my preferred machine for programming. I'm a long time linux user and switched to mac for 3-4 years now.
I enjoyed the user interface of mac os and consistency of the machine, we programmers always require a tough machine and switching machine in between is lot of hassle.



what is the use of * in python function definition
*************************************************

In python 3 you can specify * barely to force parameters after that as keyword only arguments

.. code-block:: python

    >>>def fn(arg1, arg2, *, kwarg1, kwarg2):
    ...     print(arg1, arg2, kwarg1, kwarg2)
    ... 
    >>> fn(1, 2, 3, 4)
    Traceback (most recent call last):
    File "<stdin>", line 1, in <module>
    TypeError: fn() takes 2 positional arguments but 4 were given
    >>> fn(1, 2, kwarg1=3, kwarg2=4)
    1 2 3 4
    >>> 

ref: `stackoverflow <https://stackoverflow.com/questions/36467057/what-is-the-use-of-in-python-function-definition>`_