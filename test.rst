===================
``extmath`` Doctest
===================

This doctest also help user learn ``extmath``'s features.

To experiment with this module, import it first.

>>> from extmath import *

The ``import *`` is just for convenience, since every items will be tested.

Help from other modules also needed, but not ``import *`` to prevent collision.

>>> import math
>>> import itertools

Constance
=========

Single Value
------------

>>> pi
3.141592653589793
>>> phi
1.618033988749895

List of Vaules
--------------

>>> fibonaccis
[1, 1, ...]
>>> primes
[2, 3, ...]

The list will not growth until element beyond the last one is needed.

>>> fibonaccis[10]
89
>>> fibonaccis
[1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, ...]

Prime list works sighly difference, it may produce primes more than expected.

>>> primes[5]
13
>>> primes
[2, 3, 5, 7, 11, 13, 17, 19, 23, ...]

Slicing list to get exact number of elements are possible, however.

>>> primes[:12]
[2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37]

Take some values with ``primes.under``, this is same to ``itertools.takewhile``.

>>> list(primes.under(53))
[2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47]
>>> list(itertools.takewhile(lambda x: x < 53, primes))
[2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47]

Function
========

Prime-Number Relate
-------------------

Prime-Counting Function ``pi`` (share name with the constance).

>>> [pi(i) for i in range(20)]
[0, 0, 1, 2, 2, 3, 3, 4, 4, 4, 4, 5, 5, 6, 6, 6, 6, 7, 7, 8]
>>> pi(100)
25
>>> for i in itertools.count():
...     if pi(i) > 100:
...         print(i)
...         break
... 
547

This is also equalence to

>>> primes[100]
547

To test whether n is prime, use ``in`` keyword.

>>> 43 in primes
True
>>> 1007 in primes
False

Factorization with ``factorized``.

>>> factorized(42)
[2, 3, 7]

To get list of all dividable, use ``divisors``.

>>> divisors(42)
[1, 2, 3, 6, 7, 14, 21, 42]

Ohter divisor function such as ``sigma`` is subscriptable.

>>> sigma[0](42)
8
>>> sigma[1](42)
96
>>> sigma(42) == sigma[1](42)
True

``phi``, also known as Euler totient, will show number of relatively primes.

>>> phi(42)
12
>>> phi(43)
42

Working with List of Numbers
----------------------------

``product`` works like builtin's ``sum``, except each numbers will be multiply.

>>> product([1, 2, 3, 4, 5])
120

While ``sumpow`` doesn't takes full list, it require just the last one.
and assume this list start from 1, with 1 step.

>>> sumpow(100)
5050
>>> sumpow(1234567890)
762078938126809995

It's can also power each number like this

>>> sum(i**2 for i in range(1, 11))
385
>>> sumpow(10, 2)
385

``sumexp`` will find geometric sum, ``r**0 + r**1 + r**2 + ... + r**k``.

>>> sumexp(2, 10)
2047

Extended Class
--------------

``Fraction.decimal`` will string of exact (repeating) decimal of the fraction.

>>> Fraction(1, 2).decimal()
'0.5'
>>> Fraction(1, 7).decimal()
'0.(142857)'
>>> Fraction(23, 42).decimal()
'0.5(476190)'

Change the wrapper of repeating part by supplying string as argument.

>>> Fraction(23, 42).decimal('.')
'0.5...476190...'
>>> Fraction(23, 42).decimal('~~')
'0.5~476190~'

Given ``None`` to show repeating part twice, with trailing ellipsis.

>>> Fraction(23, 42).decimal(None)
'0.5476190476190...'

Meta
====

To create duality value-function data, use ``@duality`` as function decorator.

>>> @duality(1.23456789)
... def geek(n):
...     return 1.0 / n**2 + 1.0 / n
...
>>> geek * 5
6.17283945
>>> geek(9)
0.12345679012345678

This is quite same to infinite list, except you need to ``return locals()``.

>>> @infinitelist([0, 1, 4, 9])
... def sequence(class_base):
...     def __generate__(self):
...         self.append(len(self) ** 2)
...     return locals()
...
>>> sequence
[0, 1, 4, 9, ...]
>>> sequence[10]
100
>>> sequence
[0, 1, 4, 9, 16, 25, 36, 49, 64, 81, 100, ...]

The ``__generate__`` method is just for convenience, it will be called when
element at desirable index is not yet create.
