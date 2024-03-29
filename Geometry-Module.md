# Geometry Module

<!-- wikitest release,master -->

## Introduction

The geometry module for SymPy allows one to create two-dimensional geometrical entities, such as lines and circles, and query information about these entities. This could include asking the area of an ellipse, checking for collinearity of a set of points, or finding the intersection between two lines. The primary use case of the module involves entities with numerical values, but it is possible to also use symbolic representations.

## Available Entities

The following entities are currently available in the geometry module:

* Point
* Line, Ray, Segment
* Ellipse, Circle
* Polygon, RegularPolygon, Triangle

Most of the work one will do will be through the properties and methods of these entities, but several global methods exist for one's usage:

* intersection(entity1, entity2)
* are_similar(entity1, entity2)
* convex_hull(points)

For a full API listing and an explanation of the methods and their return values please view the documentation that comes with SymPy or visit the API listing available in the [git repository](https://github.com/sympy/sympy).

## Example Usage
The following Python session gives one an idea of how to work with some of the geometry module.

    >>> from sympy.geometry import *
    >>> x = Point(0, 0)
    >>> y = Point(1, 1)
    >>> z = Point(2, 2)
    >>> zp = Point(1, 0)
    >>> Point.is_collinear(x, y, z)
    True
    >>> Point.is_collinear(x, y, zp)
    False
    >>> t = Triangle(zp, y, x)
    >>> t.area
    1/2
    >>> t.medians[x]
    Segment(Point(0, 0), Point(1, 1/2))
    >>> m = t.medians
    >>> intersection(m[x], m[y], m[zp])
    [Point(2/3, 1/3)]
    >>> c = Circle(x, 5)
    >>> l = Line(Point(5, -5), Point(5, 5))
    >>> c.is_tangent(l) # is l tangent to c?
    True
    >>> l = Line(x, y)
    >>> c.is_tangent(l) # is l tangent to c?
    False
    >>> intersection(c, l)
    [Point(-5*2**(1/2)/2, -5*2**(1/2)/2), Point(5*2**(1/2)/2, 5*2**(1/2)/2)]


## Intersection of medians

    >>> from sympy import Symbol
    >>> from sympy.geometry import *
    >>> a = Symbol("a")
    >>> b = Symbol("b")
    >>> c = Symbol("c")
    >>> x = Point(0,0)
    >>> y = Point(c,0)
    >>> z = Point(a,b)
    >>> t = Triangle(x,y,z)
    >>> t.area
    b*c/2

    >>> t.medians
    {Point(a, b): Segment(Point(a, b), Point(c/2, 0)), Point(c, 0): Segment(Point(c, 0), Point(a/2, b/2)), Point(0, 0): Segment(Point(0, 0), Point(a/2 + c/2, b/2))}

    >>> intersection(t.medians[x], t.medians[y], t.medians[z])
    []


## An in-depth example: Pappus' Theorem

    >>> from sympy import *
    >>> from sympy.geometry import *
    >>> l1 = Line(Point(0, 0), Point(5, 6))
    >>> l2 = Line(Point(0, 0), Point(2, -2))

    >>> def subs_point(l, val):
    ...     """Take an arbitrary point and make it a fixed point."""
    ...     t = Symbol('t')
    ...     ap = l.arbitrary_point()
    ...     return Point(ap[0].subs(t, val), ap[1].subs(t, val))

    >>> p11 = subs_point(l1, 5)
    >>> p12 = subs_point(l1, 6)
    >>> p13 = subs_point(l1, 11)
    >>>
    >>> p21 = subs_point(l2, -1)
    >>> p22 = subs_point(l2, 2)
    >>> p23 = subs_point(l2, 13)
    >>>
    >>> ll1 = Line(p11, p22)
    >>> ll2 = Line(p11, p23)
    >>> ll3 = Line(p12, p21)
    >>> ll4 = Line(p12, p23)
    >>> ll5 = Line(p13, p21)
    >>> ll6 = Line(p13, p22)
    >>>
    >>> pp1 = intersection(ll1, ll3)[0]
    >>> pp2 = intersection(ll2, ll5)[0]
    >>> pp3 = intersection(ll4, ll6)[0]
    >>>
    >>> print Point.is_collinear(pp1, pp2, pp3)
    True


## Miscellaneous Notes

* The area property of Polygon and Triangle may return a positive or negative value, depending on whether or not the points are oriented counter-clockwise or clockwise, respectively. If you always want a positive value be sure to use the `abs` function.
* Although Polygon can refer to any type of polygon, the code has been written for simple polygons. Hence, expect potential problems if dealing with complex polygons (overlapping sides).
* Since !SymPy is still in its infancy some things may not simplify properly and hence some things that should return True (e.g., Point.is_collinear) may not actually do so. Similarly, attempting to find the intersection of entities that do intersect may result in an empty result.

## Future Work
### Truth Setting Expressions

When one deals with symbolic entities, it often happens that an assertion cannot be guaranteed. For example, consider the following code:

    >>> from sympy import *
    >>> from sympy.geometry import *
    >>> x,y,z = map(Symbol, 'xyz')
    >>> p1,p2,p3 = Point(x, y), Point(y, z), Point(2*x*y, y)
    >>> Point.is_collinear(p1, p2, p3)
    False

Even though the result is currently `False`, this is not _always_ true. If the quantity `z - y - 2*y*z + 2*y**2 == 0` then the points will be collinear. It would be really nice to inform the user of this because such a quantity may be useful to a user for further calculation and, at the very least, being nice to know. This could be potentially done by returning an object (e.g., !GeometryResult) that the user could use. This actually would not involve an extensive amount of work and therefore may be implemented by the end of SoC '07.

### Three Dimensions and Beyond
Currently there are no plans for extending the module to three dimensions, but it certainly would be a good addition. This would probably involve a fair amount of work since many of the algorithms used are specific to two dimensions.

### Geometry Visualization
The plotting module is capable of plotting geometric entities. See [[Plotting_Module#Plotting_Geometric_Entities|Plotting Geometric Entities]] in the plotting module entry.

