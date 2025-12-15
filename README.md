Interactive Bézier Curve with Spring Physics
Overview

This project implements an interactive cubic Bézier curve that behaves like a flexible rope. The curve responds in real time to mouse movement, while visualizing both the curve and its tangent vectors.
All Bézier mathematics, physics simulation, and rendering logic are implemented manually, without using any prebuilt Bézier, animation, or physics libraries.

Mathematical Model
Cubic Bézier Curve

The curve is defined by four control points:

P₀, P₃: fixed endpoints

P₁, P₂: dynamic control points influenced by physics

For a parameter 
𝑡
∈
[
0
,
1
]
t∈[0,1], the cubic Bézier curve is evaluated as:

𝐵
(
𝑡
)
=
(
1
−
𝑡
)
3
𝑃
0
+
3
(
1
−
𝑡
)
2
𝑡
𝑃
1
+
3
(
1
−
𝑡
)
𝑡
2
𝑃
2
+
𝑡
3
𝑃
3
B(t)=(1−t)
3
P
0
	​

+3(1−t)
2
tP
1
	​

+3(1−t)t
2
P
2
	​

+t
3
P
3
	​


In the implementation, the curve is rendered by sampling 
𝑡
t at regular intervals (Δt ≈ 0.02) and drawing a polyline through the computed points.

Tangent Computation

To visualize the direction and curvature of the Bézier curve, tangent vectors are computed using the analytical derivative:

𝐵
′
(
𝑡
)
=
3
(
1
−
𝑡
)
2
(
𝑃
1
−
𝑃
0
)
+
6
(
1
−
𝑡
)
𝑡
(
𝑃
2
−
𝑃
1
)
+
3
𝑡
2
(
𝑃
3
−
𝑃
2
)
B
′
(t)=3(1−t)
2
(P
1
	​

−P
0
	​

)+6(1−t)t(P
2
	​

−P
1
	​

)+3t
2
(P
3
	​

−P
2
	​

)

Each tangent vector is normalized and drawn as a short line segment at selected points along the curve.

Physics Model
Spring–Damping System

The dynamic control points P₁ and P₂ follow a mass–spring–damper model to achieve smooth, rope-like motion.

The acceleration is calculated as:

𝑎
=
𝑘
(
𝑥
𝑡
𝑎
𝑟
𝑔
𝑒
𝑡
−
𝑥
)
−
𝑑
𝑣
a=k(x
target
	​

−x)−dv

Where:

𝑘
k is the spring stiffness

𝑑
d is the damping coefficient

𝑣
v is velocity

𝑥
𝑡
𝑎
𝑟
𝑔
𝑒
𝑡
x
target
	​

 is the target position derived from user input

Velocity and position are updated using explicit Euler integration:

𝑣
←
𝑣
+
𝑎
⋅
𝑑
𝑡
v←v+a⋅dt
𝑥
←
𝑥
+
𝑣
⋅
𝑑
𝑡
x←x+v⋅dt

This produces smooth motion with natural lag and prevents abrupt snapping.

Interaction Design

Mouse movement determines the target positions of the dynamic control points.
Instead of directly following the mouse, each control point moves toward a blended target position, creating a visually realistic rope effect where the curve appears to be influenced rather than rigidly dragged.

Rendering Pipeline

Each animation frame performs the following steps:

Update physics for control points P₁ and P₂

Sample the Bézier curve

Render the curve path

Render tangent vectors

Render control points

Rendering is handled using the HTML Canvas API and requestAnimationFrame, maintaining approximately 60 FPS.

Design Choices

Manual Bézier math ensures full mathematical transparency

Spring–damping physics provides realistic motion with minimal complexity

Fixed endpoints simplify constraints and stabilize the curve

Normalized tangents ensure consistent direction visualization

No external libraries are used, strictly following assignment rules

Performance Considerations

Curve sampling is limited to ~50 points per frame

Tangents are drawn at fewer intervals to reduce overhead

Physics updates are constant-time

Canvas redraws remain lightweight and stable in real time

Conclusion

This implementation demonstrates a complete integration of mathematical modeling, physics-based animation, and interactive graphics.
The result is a responsive and efficient Bézier rope simulation that satisfies all assignment requirements while remaining optimized and easy to understand.

If you want, I can:

Shorten this to one-page submission format

Simplify it for viva explanation

Convert equations to plain-text only

Align it with a grading rubric

Just tell me what you need next.

make it humanise

Below is a human-sounding, simple, and natural version of the README.
It keeps the technical correctness, but removes the “textbook / AI” tone so it feels like you actually wrote it.

You can submit this confidently.

Interactive Bézier Curve with Spring Physics
Overview

This project demonstrates an interactive cubic Bézier curve that behaves like a flexible rope. The curve reacts smoothly to mouse movement, giving a natural, spring-like motion. Along with the curve itself, tangent directions are also visualized to show how the curve bends at different points.

All the mathematics, physics, and rendering logic are written manually, without using any built-in Bézier or physics libraries.

Bézier Curve Logic

The curve is defined using four control points:

P₀ and P₃ are fixed endpoints

P₁ and P₂ are movable control points

For a parameter 
𝑡
t between 0 and 1, the curve position is calculated using the standard cubic Bézier equation:

𝐵
(
𝑡
)
=
(
1
−
𝑡
)
3
𝑃
0
+
3
(
1
−
𝑡
)
2
𝑡
𝑃
1
+
3
(
1
−
𝑡
)
𝑡
2
𝑃
2
+
𝑡
3
𝑃
3
B(t)=(1−t)
3
P
0
	​

+3(1−t)
2
tP
1
	​

+3(1−t)t
2
P
2
	​

+t
3
P
3
	​


The curve is drawn by sampling multiple values of 
𝑡
t and connecting the computed points using straight line segments.

Tangent Visualization

To understand how the curve bends, tangents are calculated using the derivative of the Bézier equation:

𝐵
′
(
𝑡
)
=
3
(
1
−
𝑡
)
2
(
𝑃
1
−
𝑃
0
)
+
6
(
1
−
𝑡
)
𝑡
(
𝑃
2
−
𝑃
1
)
+
3
𝑡
2
(
𝑃
3
−
𝑃
2
)
B
′
(t)=3(1−t)
2
(P
1
	​

−P
0
	​

)+6(1−t)t(P
2
	​

−P
1
	​

)+3t
2
(P
3
	​

−P
2
	​

)

These tangent vectors are normalized and drawn as short line segments along the curve, clearly showing its direction and curvature.

Physics Model

The movement of control points P₁ and P₂ is based on a simple spring-damping system.

Each control point tries to move toward a target position derived from mouse input, but instead of snapping instantly, it follows physics-based motion:

𝑎
=
𝑘
(
𝑥
𝑡
𝑎
𝑟
𝑔
𝑒
𝑡
−
𝑥
)
−
𝑑
𝑣
a=k(x
target
	​

−x)−dv

Here:

𝑘
k controls how stiff the rope feels

𝑑
d controls how quickly motion settles

𝑣
v is velocity

Positions are updated using Euler integration, which gives smooth and natural movement with a slight lag, similar to a real rope.

Interaction Design

Mouse movement influences the target positions of the inner control points. Since the points move toward the mouse indirectly through the spring system, the curve feels flexible rather than rigid. This makes the interaction more realistic and visually pleasing.

Rendering Process

Each animation frame performs the following steps:

Update physics for the moving control points

Recalculate the Bézier curve

Draw the curve

Draw tangent lines

Draw control points

Rendering is done using the HTML Canvas API and requestAnimationFrame, which keeps the animation smooth at around 60 FPS.

Design Choices

Bézier math is written manually for full control and clarity

Spring-based motion keeps the animation smooth and realistic

Fixed endpoints make the rope stable and easy to control

Tangent visualization helps in understanding curve behavior

No external libraries are used, fully meeting assignment constraints

Performance Notes

The curve is sampled efficiently to avoid unnecessary computation

Physics updates are lightweight

Canvas rendering remains fast and responsive

Conclusion

This project combines mathematics, physics, and interactive graphics into a clean and efficient simulation. The final result is a smooth, responsive Bézier rope that clearly demonstrates both curve geometry and real-time motion behavior.
