Interactive Bézier Curve with Spring Physics
Introduction

A cubic Bézier curve with an interactive functionality of a flexible rope is developed in this project. The curve is capable of instantly responding to the mouse movement, with both the curve and the tangent vectors being shown.

Everything dealing with Bézier math, physics simulation, and rendering is coded by hand, without using any existing libraries for Bézier math, animation, or physics simulations.

Mathematical Model
A

Cubic Bézier Curve

The curve is described by using four control points:

P₀, P₃: Fixed endpoints
P₁, P₂: dynamic control points with physics influence
For a parameter
t
⊆

0


1
]
t∈[0,1]    The cubic Bézier curve can
X


)
=

1
−

)
3
P
0
+
3

1
−

)
2
$t
P
1
-
3

1
−

)

2
P
2
+
t
3
P
3
B(t

3
P
0
​​

3
2
TP
1

​​
3
2
P


2
​

+t

3

P
3
​
During implementation, this curve is drawn using

t at a constant time interval (Δt≈0.02) and plotting a polyline through these calculated points.
Tangent Computation
To illustrate the path the curve will take, based on a Bézier curve, calculation using the derivative function defines two vectors:

′

X
)
=
3
nergie
1
−

)
2

P
1
−
P
0
)
+
6

1
−
"t
)
function

*
2
−
P
1
)
+
3

2

P
3
−
P

2
)

A
′

(t
2

(P
1
CppClass
-P

0
​

)+

2



−P

1

​​
)+
2
P
3
​​
−P
2
​
)
A unit vector in each point of the curve is constructed and graphed using a small line segment.
Physics Model
Models
Spring-Damping System
The dynamic control points P₁ and P₂ employ a mass spring-damper model for a smooth, rope-like behavior.
Acceleration is calculated using the formula:
a
=
k






a



c



−
z
)
−
d
v
a=k

Target

​

−x
Where:
$k
k 
Spring stiffness in kN/m
d
d  
is damping coefficient

v = velocity


a
$r


$t
x
target

​​

is based on user input
is referred to as

Velocities and positions are calculated using an explicit Euler integration step:

v

→

v

+

a



d



v



→



-

W



d



$x

It leads to fluid motion with authentic lag behavior and eliminates abrupt snapping.

Interaction Design
Interaction

The positions of the dynamic control points are determined based on mouse movement.
Rather than tracking the mouse cursor directly, each control point is drawn towards a Figure Eight target point, achieving a very intuitive rope simulation where the curve is ‘influenced’ rather than ‘dragged.’ Rendering Pipeline Every frame in this animation contains these steps: Update physics for control points P₁ and P₂ Sample Bézier curve Make the curve path Representing Tangent Vectors Create control points Rendering is performed using the HTML5 Canvas API in combination with requestAnimationFrame in order to keep a constant speed of approximately 60 FPS. Design Choices
================ "By doing all calculations using Manual Bézier math, complete mathematical A physics model based on a spring and damping gives a realistic motion with less complexity Fixed endpoints make constraint statements simpler and help to stabilize a curve Normalized Tangents will make visually consistent directions No libraries are used in this code
Following rules of the assignment Technical Assessment The curve sampling is restricted to approximately 50 samples per frame Tangents will be drawn less frequently in order to cut overhead Physics updates are constant time Canvas canvas redrawning is always light and fast
  }}} Conclusion A complete integration of mathematical modeling, physics-based animation, and graphic interaction is shown in this implementation. The end product is an efficient and dynamic simulation of a Bézier rope that meets all of the requirements of the assignment.
