Interactive Bézier Curve with Spring Physics

This project implements an interactive cubic Bézier curve that behaves like a flexible rope. The curve responds smoothly to mouse movement and visualizes both the curve itself and its tangents. All mathematics, physics, and rendering logic are written manually without using any built-in Bézier or physics libraries.

The Bézier curve is defined using four control points. P₀ and P₃ are fixed endpoints, while P₁ and P₂ are dynamic control points that move based on user input and physics. For a parameter t in the range [0,1], the curve position is computed using the standard cubic Bézier equation:
B(t) = (1−t)³P₀ + 3(1−t)²tP₁ + 3(1−t)t²P₂ + t³P₃.
In the implementation, the curve is rendered by sampling t at regular intervals and connecting the evaluated points using line segments.

To visualize the direction and curvature of the curve, tangent vectors are computed using the derivative of the cubic Bézier equation:
B′(t) = 3(1−t)²(P₁−P₀) + 6(1−t)t(P₂−P₁) + 3t²(P₃−P₂).
These vectors are normalized and drawn as short line segments at selected points along the curve.

The motion of the dynamic control points P₁ and P₂ is governed by a spring-damping physics model. Each point moves toward a target position derived from mouse input using the equation a = k(x_target − x) − d·v, where k is the spring stiffness, d is the damping coefficient, and v is velocity. Velocity and position are updated using explicit Euler integration, which produces smooth motion with natural lag and prevents abrupt snapping.

Mouse movement influences the target positions of the dynamic control points. Instead of directly following the mouse, the points are pulled toward it through the spring system, creating a realistic rope-like behavior where the curve appears flexible rather than rigid.

Each animation frame updates the physics of the control points, recalculates the Bézier curve, draws the curve path, renders tangent vectors, and finally draws the control points. Rendering is performed using the HTML Canvas API with requestAnimationFrame, maintaining smooth real-time performance at approximately 60 FPS.

Manual Bézier computation ensures mathematical transparency, while the spring-damping model provides realistic motion with minimal complexity. Fixed endpoints improve stability and clarity, normalized tangents provide consistent visualization, and the absence of external libraries ensures full compliance with the assignment requirements.

This project demonstrates a clean integration of mathematical modeling, physics-based animation, and interactive graphics, resulting in a responsive and visually intuitive Bézier rope simulation.
