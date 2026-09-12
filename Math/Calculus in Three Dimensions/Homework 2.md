---
title: "Homework 1"
author: "Gustavo Grancieiro Ramalho"
fontsize: 11pt
geometry: margin=1in
papersize: letter
monofont: "JetBrainsMono Nerd Font Mono"
mainfont: "Inter"
linestretch: 1.15
---

#### Problem 1

Line $x-2=\frac{y-2}{3}=2z+1$ and plane $x-3y-z=-2$

$$x-2=\frac{y-2}{3}=\frac{z+\frac{1}{2}}{\frac{1}{2}} \implies d=\langle 1, 3, \frac{1}{2} \rangle=\langle 2, 6, 1 \rangle$$
$$n=\langle 1, -3, -1 \rangle$$
$$
\begin{aligned}
d \cdot n &= 2 + 6 \cdot -3 + 1 \cdot -1 = -17 \\
|d| &= \sqrt{4+36+1} = \sqrt{ 41 } \\
|n| &= \sqrt{1+9+1}=\sqrt{ 11 } \\
\cos \theta &= \frac{dn}{|d||n|}=-\frac{17}{\sqrt{ 41 }\sqrt{ 11 }} \\
\theta&=\arccos\left( \frac{17}{\sqrt{ 451 }} \right) \approx 36.8 \degree
\end{aligned}
$$
Hence, the angle is approximately $90 \degree - 36.8 \degree = 53.2 \degree$.

#### Problem 2

Reflect $(1, -3, 2)$ across the plane $3x-2y+z=-1$. We find the normal and the parametric equation, then plug:
$$n = (3, -2, 1)$$
$$
\begin{aligned}
x=x_{0}+at=1+3t && y=y_{0} + bt=-3-2t && z=z_{0} + ct = 2 + t
\end{aligned}
$$
$$
\begin{aligned}
3(1+3t) - 2(-3-2t) + (2+t) & =-1 \\
3 + 9t + 6 + 4t + 2 + t &= -1 \\
11 + 14t &=-1 \implies t = -\frac{6}{7}
\end{aligned}
$$
The reflection is the same distance past the plane so we use $t=-\frac{12}{7}$.
$$R=\left( 1-\frac{36}{7}, -3 + \frac{24}{7}, 2-\frac{12}{7} \right) = \left( -\frac{29}{7}, \frac{3}{7}, \frac{2}{7} \right)$$

#### Problem 3

Show that $-x-6=\frac{y}{2}-5=3z+6$ and $2x=\frac{y+2}{3}=-z-4$ intersect. Find equation of the plane that contains them.

$$
\begin{aligned}
x=&-t-6 && y=&2t+10 && z =& \frac{t}{3}-2 \\
x=&\frac{s}{2} && y =& 3s-2 && z =& -s-4
\end{aligned}
$$
$$
\begin{aligned}
d_{1} = \langle -1, 2, \frac{1}{3} \rangle=\langle-3,6,1 \rangle &&  d_{2}=\langle \frac{1}{2}, 3, -1 \rangle = \langle 1, 6, -2 \rangle
\end{aligned}
$$
$$
\begin{aligned}
-t-6=\frac{s}{2} && 2t+10=3s-2 && \frac{t}{3}-2 = -s - 4 \\
\end{aligned}
$$
Solve x, plug in y.
$$
\begin{aligned}
s=-2t-12 \\
2t + 10 = 3(-2t - 12) - 2 = -6y-38 \implies 8t=-48 \implies t = -6 \\ s=0
\end{aligned}
$$
So they intersect, now the equation. Nomrla of the plane we find perpendicular to both lines, we do the cross product.
$$
\begin{aligned}
\langle  a_{1}, a_{2}, a_{3} \rangle \times \langle b_{1}, b_{2}, b_{3} \rangle &= \langle a_{2} b_{3} - a_{3} b_{2}, a_{3} b_{1} - a_{1}b_{3}, a_{1}b_{2} = a_{2}b_{1} \rangle \\
x&=6 \cdot -2 - 6 = -12-6=-18\\
y&=1 - (-3)(-2)=1-6=-5 \\
z&=(-3)6 - 6 = -18 - 6 = -24 \\
n&= \langle -18, -5, -24 \rangle
\end{aligned}
$$
Hence
$$
\begin{aligned}
-18(x-0)-5(y+2)-24(z+4)&=0\\
-18x-5y-10-24z-96&=0 \\
-18x-5y-24z&=106
\end{aligned}
$$

#### Problem 4

Equation of the line intersection of planes $3x-2y+z=2$ and $-x+2y+z=-3$

We add to cancel out $-2y$ and $2y$ to isolate one variable
$$
\begin{aligned}
3x-2y+z-x+2y+z &= 2 - 3 \\
2x + 2z &=-1\\
x&=-\frac{1}{2}-z
\end{aligned}
$$
$$
\begin{aligned}
-\left( -\frac{1}{2} -z\right)+2y+z &= -3 \\
\frac{1}{2} + 2z + 2y &= -3 \\
y &= -\frac{7}{4} - z
\end{aligned}
$$
Now let $z=y$ and to get the parametric equation
$$
\begin{aligned}
x = -\frac{1}{2} -t && y= -\frac{7}{4} - t && z=t
\end{aligned}
$$

#### Problem 5

Rotate $-x+3y+z=2$ by $90 \degree$ about the line $\langle 2 + t, 2 + 2t, -1 + 2t \rangle$

We rotate the normal $n=\langle -1, 3, 1 \rangle$ and the point. Axis is $(2, 2, -1)$ direction $d = \langle 1, 2, 2 \rangle$, $|d|=\sqrt{ 1 + 4 + 4 } = 3$.
$$
\begin{aligned}
v'=\operatorname{proj}_{u}v+(v-\operatorname{proj}_{u}v)\cos \theta + \operatorname{rot}_{u}v\sin \theta \\
\operatorname{rot}_{u}v = \frac{u \times v}{|u|}\\
\theta = 90 \degree \\
\cos \theta = 0 \\
\sin \theta = 1
\end{aligned}
$$
$$
\begin{aligned}
\operatorname{proj}_{d}n=\frac{n \cdot d}{d \cdot d}d = \frac{-1 + 6 + 2}{9} \langle 1, 2, 2 \rangle = \langle \frac{7}{9}, \frac{14}{9} \frac{14}{9} \rangle
\end{aligned}
$$
$$
\begin{aligned}
n \times d = \langle 1, 2, 2 \rangle \times \langle-1, 3, 1 \rangle \\
x = -4 \\
y = -3 \\
z = 5 \\
\operatorname{rot}_{d}n=\frac{\langle -4, -3, -5 \rangle}{3}=\langle -\frac{4}{3}, -1, \frac{5}{3} \rangle \\
n' = \langle \frac{7}{9} - \frac{12}{9}, \frac{14}{9} - 1, \frac{14}{9} + \frac{15}{9} \rangle = \langle-\frac{5}{9}, \frac{5}{9}, \frac{29}{9} \rangle
\end{aligned}
$$
Now the point we find where the axis meets the plane
$$ \begin{aligned} -(2+t)+3(2+2t)+(-1+2t) &= 2 \\ 3+7t &= 2 \\ t &= -\tfrac17 \end{aligned}$$
Hence rotation is $\left(\tfrac{13}{7},\ \tfrac{12}{7},\ -\tfrac97\right)$. Equation:
$$ -\tfrac59\left(x-\tfrac{13}{7}\right)+\tfrac59\left(y-\tfrac{12}{7}\right)+\tfrac{29}{9}\left(z+\tfrac97\right) = 0 $$
#### Problem 6

Distance between $-x+2=\frac{y}{2} + 1=z+2$ and $\frac{x+2}{3}=\frac{y}{2}=z$

Pick a point on each line
$$
\begin{aligned}
d_1 &= \langle -1,2,1\rangle, & P_1 &= (2,-2,-2) \\
d_2 &= \langle 3,2,1\rangle,  & P_2 &= (-2,0,0)
\end{aligned}
$$
The distance is the length of the shortest segment joining the lines, which is perpendicular to both lines, so parallel to $d_1\times d_2$. Take any vector from one line to the other and project it onto that direction.

$$
\begin{aligned}
n &= d_1\times d_2 = \left\langle 2(1)-1(2),\ 1(3)-(-1)(1),\ (-1)(2)-2(3)\right\rangle = \langle 0,4,-8\rangle \\
P_1P_2 &= \langle -2-2,\ 0-(-2),\ 0-(-2)\rangle = \langle -4,2,2\rangle \\
\text{dist} &= \frac{\left|P_1P_2\cdot n\right|}{| n|} = \frac{|0+8-16|}{\sqrt{0+16+64}} = \frac{8}{4\sqrt5} = \frac{2}{\sqrt5}
\end{aligned}
$$

#### Problem 7

$a \neq 0$ Show that if $a \cdot b = a \cdot c$ and $a \times b = a \times c$ then $b = c$ (a,  b, c are vectors)

$a(b-c)=ab - ac = 0$
$a \times (b-c) = a \times b - a \times c = 0$

Also:

$a(b-c)=|a||b-c|\cos \theta=0$ and $|a \times (b-c)|=|a||b-c|\sin \theta = 0$

Since $a \neq 0$ we can divide it out from both. Now if $b-c \neq 0$ we could also divide $|b-c|$ but that would leave $\cos \theta = 0$ and $\sin \theta = 0$, and both of them can’t be true at the same time. Hence $(b-c)=0$. That is, $b=c$.

#### Problem 8

Three mirrors meet at right angles. Show incoming ray of light is reflected by these three mirrors in exactly the opposite direction that it came from.

We take the mirrors as the planes $x=0$, $y=0$ and $z=0$ and with normals equal to the unit vectors $i,j,k$. Say the ray travels in $v= \langle a, b, c \rangle$. Reflecting off a flat mirror with normal $n$ reverses the components of $v$ along the normal and leaves the parallel parts alone.
$$
v'=v-2\operatorname{proj}_{n}v = v-2(v \cdot n)n
$$
For mirror $z$:
$$v'=\langle a, b, c\rangle-2(vk)\langle 0,0,1\rangle=\langle a,b,-c\rangle$$
Likewise for mirrors $x$ and $y$, they will effect $v’=\langle -a, -b, -c \rangle$. So the outgoing ray will point opposite to the incoming one.

#### Problem 9

**Part 1.** Show $\frac{d}{dt}(u(t) \times v(t))=\frac{du(t)}{dt} \times v(t) + u(t) \times \frac{dv(t)}{dt}$. 

Let $u=\langle u_1, u_{2}, u_{3} \rangle$ and $v=\langle v_{1}, v_{2}, v_{3} \rangle$, then:
$$
u \times v = \langle u_{2}v_{3}-u_{3}v_{2}, u_{3}v_{1}-u_{1}v_{3}, u_{1}v_{2}-u_{2}v_{1} \rangle
$$
We differentiate each component:
$$\begin{aligned}  
(u_2v_3-u_3v_2)' &= u_2'v_3+u_2v_3'-u_3'v_2-u_3v_2' = (u_2'v_3-u_3'v_2)+(u_2v_3'-u_3v_2')\\  
(u_3v_1-u_1v_3)' &= u_3'v_1+u_3v_1'-u_1'v_3-u_1v_3' = (u_3'v_1-u_1'v_3)+(u_3v_1'-u_1v_3')\\  
(u_1v_2-u_2v_1)' &= u_1'v_2+u_1v_2'-u_2'v_1-u_2v_1' = (u_1'v_2-u_2'v_1)+(u_1v_2'-u_2v_1')  
\end{aligned}$$
In each row the first parenthesis is $u' \times v$ and the second is $v' \times u$. So $( u\times v)' = u'\times v+ u\times v'$.

**Part 2**. Show that if $r(t)$ is always parallel to $\frac{d^2r(t)}{dt^2}$ then $r(t) \times \frac{dr(t)}{dt}$ is constant.

We apply the rule above with $u=r$ and $v=r’$:
$$
\frac{d}{dt}(r \times r')=r' \times r' + r \times r''
$$
The first term is $0$ because any vector cross with itself is $0$. The second term is 0 because $r$ is parallel to $r’’$ and the cross product of parallel vectors is 0 (since $\sin 0 = 0$). So the derivative is $0$ hence a constant.