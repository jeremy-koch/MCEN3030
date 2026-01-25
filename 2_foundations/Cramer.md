# Cramer's Rule and Motivation for Matrix Methods

Solving a linear system $\mathbf{A}\mathbf{x}=\mathbf{b}$ for unknown $\mathbf{x}$ is "the" linear algebra problem. For a square matrix $\mathbf{A}$, the solution is
$$
\mathbf{x}=\mathbf{A}^{-1}\mathbf{b}.
$$
Easy, right? It turns out that calculating the inverse of a matrix is computationally very expensive. We'll see a hint as to why here.


## Cramer's Rule
For a linear system $\mathbf{A}\mathbf{x}=\mathbf{b}$, with $\mathbf{x}=[x_1, x_2, x_3, ... , x_N]^T$, the value of $x_n$ will be given by
$$
x_n = \frac{\text{det}(\mathbf{A}_n)}{\text{det}(\mathbf{A})}
$$
where $\mathbf{A}_n$ is the matrix formed by replacing the $n^\text{th}$ column in $\mathbf{A}$ with $\mathbf{b}$. A quick example: if
\begin{equation}
\begin{bmatrix}
2 & 0\\ -1 & 1
\end{bmatrix}
\begin{bmatrix}
x \\ y
\end{bmatrix}
=
\begin{bmatrix}
3 \\ 1
\end{bmatrix}
\end{equation}
then
\begin{equation}
x = \frac{\text{det}\left(
\begin{bmatrix}
3 & 0\\ 1 & 1
\end{bmatrix}
\right)}{\text{det}\left(
\begin{bmatrix}
2 & 0\\ -1 & 1
\end{bmatrix}
\right)}
\end{equation}
and
\begin{equation}
y = \frac{\text{det}\left(
\begin{bmatrix}
2 & 3\\ -1 & 1
\end{bmatrix}
\right)}{\text{det}\left(
\begin{bmatrix}
2 & 0\\ -1 & 1
\end{bmatrix}
\right)}.
\end{equation}

## Calculating the determinant, and FLOPs

Computer performance is sometimes measured in FLOPs per second -- floating point operations (addition, multiplication etc. of floats) per second. A personal computer might be capable of 1000 gigaFLOPs per second ($10^{12}$ FLOPs/sec). Let's keep this number in mind.


For a $2\times 2$ matrix, the determinant is calculated with:
\begin{equation}
\text{det}\left(
\begin{bmatrix}
a_{11} & a_{12}\\ a_{21} & a_{22}
\end{bmatrix}
\right) = a_{11}a_{22}-a_{12}a_{21}.
\end{equation}
So, $3$ FLOPs.

For a $3\times 3$ matrix:
\begin{equation}
\text{det}\left(
\begin{bmatrix}
a_{11} & a_{12} & a_{13}\\ a_{21} & a_{22} & a_{23}\\
a_{31} & a_{32} & a_{33}
\end{bmatrix}
\right) = a_{11}\text{det}\left(
\begin{bmatrix}
a_{22} & a_{23}\\ a_{32} & a_{33}
\end{bmatrix}
\right)\\
-a_{12}\text{det}\left(
\begin{bmatrix}
a_{21} & a_{23}\\ a_{31} & a_{33}
\end{bmatrix}
\right)
+a_{13}\text{det}\left(
\begin{bmatrix}
a_{21} & a_{22}\\ a_{31} & a_{32}
\end{bmatrix}
\right).
\end{equation}
So, each of the $2\times 2$ determinants takes $3$ FLOPs, and then each of those is multiplied by something, and then we add the results together. Maybe there is some subtlety here, but for the point of this demonstration: $(3)(3)(2)= 18$ FLOPs.

For a $4\times 4$ matrix, we will need to calculate the determinant of four $3\times 3$ matrices, each takes 18 FLOPs, then four multiplications, then three additions. $(18)(4)(3)=216$ FLOPs.


For a $5\times 5$: $(216)(5)(4)=4320$. 

For a $6\times 6$: $(4320)(6)(5)=129600$. 

For a $7\times 7$: $5443200$. This isn't really even a large system yet!

For an $N\times N$ matrix: $3N!(N-1)!/2$.


In engineering, e.g. in a finite-element analysis, it would not be unreasonable (and still not that big) to have a $500\times 500$ matrix. $3N!(N-1)!/2$ with $N=500$ is 
$$
4466201622
4189812326
5086569612
0519345854\\
7202507990
9234976578
4489339089
4575441168\\
2689786180
5906290490
5656312051
4443654755\\
4930620936
2288949089
1244300239
9337669587\\
0438338361
0914162116
7594194263
0741109577\\
9297933535
5427888826
1795126255
2302832494\\
4097254659
1458576409
0262646003
7028273551\\
2180966805
0595507178
7874305286
4298812953\\
1875907971
5637542761
2363882034
2684244171\\
2497082191
1175391896
0690446382
1764026413\\
3277921574
7997637893
1564771000
7975405099\\
5282492083
3571561264
4348584705
4490987115\\
7151342158
0122517497
7717592409
8774844826\\
6451067760
9318635628
9534940392
8020644744\\
6875063037
5219095234
9155673257
6574384497\\
2719339357
5923079158
7381959160
2715129001\\
4899396412
7542782049
6419842909
5815201746\\
9497047781
4732324641
7374890396
8570838906\\
1531802777
2411497938
0439051486
6030516552\\
7145201409
5332854985
6968120718
8828164871\\
8172968127
6502071633
1472546706
6742275153\\
0695575028
7527575414
0820192131
5262018838\\
7898836040
2727548277
9973045018
8459663413\\
7221703972
5580059452
3620323014
9099864283\\
7294600312
8689911384
1656088190
5087934483\\
1797911146
2832410526
2837448607
9817032648\\
1749351722
0779540960
8591720389
2467760526\\
3322856478
2182046616
8687667347
0461833863\\
5334512229
9192742778
3775510922
2237121628\\
5414368451
5087617233
2553978213
2854541329\\
1068698630
4984245046
9795888390
6950361917\\
3980139368
5103658285
8913372393
6174659681\\
6616131365
9798902174
2655560025
1849710206\\
2720465344
6733275917
7114411494
2148147009\\
6872729536
9888143782
9092345015
4389177636\\
9482633358
0443595468
9592743655
1969923813\\
2309160708
1127069848
3107447822
1619350981\\
9381569580
4559116745
5634306877
0229223551\\
2878007187
5336134572
7313876478
6960108219\\
6785223899
2821247302
2057846467
9944687460\\
3139512903
1128931260
4412082010
1255658196\\
2613714454
6610443053
3158806709
5166956324\\
3391068207
1926197240
7672335403
0713683814\\
6164560718
8382002391
4319296720
5864766093\\
3431120129
4150215709
0832243471
7701637729\\
9309074311
2759940915
0010112638
2750523983\\
2387062465
6301463310
0731809149
1754691721\\
4816723968
4651432582
1687054391
0601377869\\
7880646814
4660509671
5522887308
1001103196\\
5541003798
3074410851
5965168160
5809953084\\
6775046027
2189164748
8000000000
0000000000\\
0000000000
0000000000
0000000000
0000000000\\
0000000000
0000000000
0000000000
0000000000\\
0000000000
0000000000
0000000000
0000000000\\
0000000000
0000000000
0000000000
0000000000\\
0000000000
0000000000
0000000000
0000000000\\
0000000000
0000000000
000000.
$$
That is: $4.5 \times 10^{2265}$. At $10^{12}$ FLOPs/sec, it would take $1.4 \times 10^{2246}$ years to complete this calculation.
:::{attention}
It is estimated that there are about $10^{80}$ atoms in the universe.

The Big Bang occurred $13.8 \times 10^{9}$ years ago.

If every atom in the universe was a tiny computer capable of performing $10^{12}$ FLOPs/sec, it would take $10^{2156}$ times the age of the universe to complete this calculation.
:::
This suggests, QUITE strongly, that a computer is not using Cramer's Rule to solve $\mathbf{A}\mathbf{x}=\mathbf{b}$. 

If you want to see for yourself: The following code will calculate the determinant of a random $500\times 500$ matrix. It probably takes about one second.
::::{tab-set}
:::{tab-item} MATLAB
```matlab
det(rand(500,500))
```
:::


:::{tab-item} python
```python
import numpy as np
d=np.linalg.det(np.random.rand(500, 500))
print(D)
```

:::


:::{tab-item} Julia
```julia
using LinearAlgebra
d = det(rand(500, 500))
println(d)
```
:::

::::