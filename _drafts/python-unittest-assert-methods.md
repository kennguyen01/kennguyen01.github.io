---
title: Python unittest Assert Methods
date: 
categories: programming
---

This post contains the assert methods listed in the documentation for Python [unittest](https://docs.python.org/3.6/library/unittest.html) module. It's a quick reference so I don't have to scroll through the docs to find a specific statement.

## Commonly Used

| Method                     |Checks that             |
|----------------------------|------------------------|
| assertEqual(a, b)          | a  ==  b               |
| assertNotEqual(a,  b)      | a  !=  b               |
| assertTrue(x)              | bool(x)  is  True      |
| assertFalse(x)             | bool(x)  is  False     |
| assertIs(a,  b)            | a  is  b               |
| assertIsNot(a,  b)         | a  is  not  b          |
| assertIsNone(x)            | x  is  None            |
| assertIsNotNone(x)         | x  is  not  None       |
| assertIn(a,  b)            | a  in  b               |
| assertNotIn(a,  b)         | a  not  in  b          |
| assertIsInstance(a,  b)    | isinstance(a,  b)      |
| assertNotIsInstance(a,  b) | not  isinstance(a,  b) |

## Exceptions, Warnings, and Logs

| Method                                            | Checks that                                                        |
|---------------------------------------------------|------------------------------------------------------------------|
| assertRaises(exc,  fun,  *args,  **kwds)          | fun(*args,  **kwds)  raises exc                                  |
| assertRaisesRegex(exc,  r,  fun,  *args,  **kwds) | fun(*args,  **kwds)  raises exc<br /> and the message matches regex r  |
| assertWarns(warn, fun, *args, **kwds)             | fun(*args, **kwds) raises warn                                   |
| assertWarnsRegex(warn,  r,  fun,  *args,  **kwds) | fun(*args,  **kwds)  raises warn<br /> and the message matches regex r |
| assertLogs(logger, level)                         | The with  block logs on logger with<br /> minimum level                |

## Specific Checks

| Method                      | Checks that                                                                         |
|-----------------------------|------------------------------------------------------------------------------------|
| assertAlmostEqual(a,  b)    | round(a-b,  7)  ==  0                                                              |
| assertNotAlmostEqual(a,  b) | round(a-b,  7)  !=  0                                                              |
| assertGreater(a,  b)        | a > b                                                                              |
| assertGreaterEqual(a, b)    | a  >=  b                                                                           |
| assertLess(a,  b)           | a  <  b                                                                            |
| assertLessEqual(a,  b)      | a <= b                                                                             |
| assertRegex(s,  r)          | r.search(s)                                                                        |
| assertNotRegex(s,  r)       | not  r.search(s)                                                                   |
| assertCountEqual(a, b)      | a and b have the same elements in the<br /> same number, regardless of their order |

## Type-Specific

| Method                     | Used to Compare    |
|----------------------------|--------------------|
| assertMultiLineEqual(a, b) | strings            |
| assertSequenceEqual(a,  b) | sequences          |
| assertListEqual(a, b)      | lists              |
| assertTupleEqual(a, b)     | tuples             |
| assertSetEqual(a,  b)      | sets or frozensets |
| assertDictEqual(a,  b)     | dicts              |