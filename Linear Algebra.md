## Getting Started
#### Understand and solve the four central problems of linear algebra:
- Linear systems: Ax = b, n by n, ch1-2
- Least squares: Ax = b, m by n, ch3-4
- Eignevalues: Ax = $\lambda$x, n by n, ch5-6
- Singular values: Av = $\sigma$u, m by n, ch7-8

#### The four fundamental subspaces lead to the Fundamental Theorem of Linear Algebra:
1. The dimensions of the four subspaces
2. The orthogonality of the two pairs
3. The best bases for all four subspaces

#### Six Great Theorems of Linear Algebra
- Dimension Theorem
	- All bases for a vector space have the same number of vectors.
- Counting Theorem
	- Dimension of column space + dimension of nullspace = number of columns.
- Rank Theorem
	- Dimension of column space = dimension of row space. This is the rank.
- Fundamental Theorem
	- The row space and nullspace of A are orthogonal complements in $R^n$. 
- Singular Value Decomposition (SVD)
	- There are orthonormal bases ($v$'s and $u$'s' for the row and column spaces) so that $Av_{i}= \sigma_{i}u_{i}$. 
- Spectral Theorem
	- If $A^{T}= A$ there are orthonormal $q$'s so that $Aq_{i}= \lambda_{i}q_{i}$ and $A = Q\Lambda Q^T$. 

#### Linear Algebra in a Nutshell: The matrix $A$ is $n$ by  $n$
| Nonsingular | Singular |
| ------------ | -------- |
| A is invertible | A is not invertible |
| The columns are independent | The columns are dependent |
| The rows are independent | The rows are dependent |
| The determinant is not zero | The determinant is zero |
| $Ax = 0$ has one solution $x = 0$ | $Ax = 0$ has infinitely many solutions |
| $Ax = b$ has one solution $x = A^{-1}b$ | $Ax = b$ has no solution or infinitely many |
| $A$ has $n$ (nonzero) pivots | A has $r<n$ pivots |
| $A$ has full rank $r = n$ | $A$ has rank $r<n$ |
| The reduced row echelon form is $R = I$ | $R$ has at least one zero row |
| The column space is all of $R^n$ | The column space has dimension $r<n$ |
| The row space is all of $R^n$ | The row space has dimension $r<n$ |
| All eigenvalues are nonzero | Zero is an eigenvalue of $A$ |
| $A^{T}A$ is symmetric positive definite | $A^{T}A$ is only semidefinite |
| $A$ has $n$ (positive) singular values | $A$ has $r<n$ singular values |


## 1 Introduction to Vectors
#### 1.1 Vectors and Lineat Combinations
1. A vector $v$ in two-dimensional space has two components $v_1$ and $v_2$.
2. $v + w = (v_{1} + w_{1}, v_{2}+ w_{2})$ and $cv = (cv_{1}, cv_{2})$ are found a component at a time.
3. A linear combination of three vectors $u$ and $v$ and $w$ is $cu + dv + ew$.
4. Take all linear combinations of $u$, or $u$ and $v$, or $u, v, w$. in three dimensions, those combinations typically fill a line, then a plane, then the whole space $R^3$.

#### 1.2 Lenghts and Dot Products
1. The dot product $v \cdot w$  multiplies each component $v_i$ by $w_i$ and adds all $v_{i}w_{i}$.
2. The length $||v||$ is the square root of $v\cdot v$. Then $u = v/||v||$ is a unit vector: length 1.
3. The dot product is $v\cdot w = 0$ when vectors $v$ and $w$ are perpendicular.
4. The cosine of $\theta$ (the angle between any nonzero $v$ and $w$) never exceeds 1:
	- Cosine: $\cos(\theta) = \frac{v\cdot w}{||v||||w||}$ 
	- Schwarz inequality: $|v \cdot w| \le ||v|| ||w||$        

#### 1.3 Matrices
1. Matrix times vector: $Ax =$ combination of the columns of $A$.
2. The solution to $Ax = b$ is $x = A^{-1}b$, when $A$ is an invertible matrix.
3. The cyclic matrix $C$ has no inverse. Its three columns lie in the same plane. Those dependent columns add to the zero vector. $Cx = 0$ has many solutions.
4. This section is looking ahead to key ideas, not fully explained yet.
 
## 2 Solving Linear Equations
#### 2.1 Vectors and Linear Equations
1. The basic operations on vectors are multiplication $cv$ and the vector addition $v + w$.
2. Together those operations give linear combinations $cv + dw$.
3. Matrix-vector multiplication $Ax$ can be computed by dot products, a row at a time. But $Ax$ must be understood as a combination of the columns of $A$.
4. Column picture: $Ax = b$ asks for a combination of columns to produce $b$.
5. Row picture: Each equation in $Ax = b$ gives a line $(n = 2)$ or a plane $(n = 3)$ or a "hyperplane" $(n > 3)$. They intersect at the solution or solutions, if any.

#### 2.2 The Idea of Elimination
1. A linear system $(Ax = b)$ becomes **upper triangular** $(Ux = c)$ after elimination.
2. We subtract $l_{ij}$ times equation $j$ from equation $i$, to make the $(i, j)$ entry zero.
3. The multiplier is $l_{ij} =$ (entry to eliminate in row $i$) / (pivot in row $j$). Pivots cannot be zero!
4. When zero is in the pivot position, exchange rows if there is a nonzero below it.
5. The upper triangular $Ux = c$ is solved by **back substitution** (starting at the bottom).
6. When **breakdown** is permanent, $Ax = b$ has no solution or infinitely many.

#### 2.3 Elimination Using Matrices
1. $Ax = x_1$ times column 1 $+ ... + x_n$  times column $n$. And $(Ax)_{i}= \sum_{j=1}^{n} a_{ij}x_{j}$.
2. Identity matrix $= I$, elimination matrix $= E_{ij}$ using $l_{ij}$, exchange matrix $= P_{ij}$.
3. Multiplying $Ax = b$ by $E_{21}$ subtracts a multiple $l_{21}$ of equation 1 from equation 2. The number $-l_{21}$ is the $(2, 1)$ entry of the elimination matrix $E_{21}$.
4. For the augmented matrix $[A\ b]$, that elimination step gives $[E_{21}A\ E_{21}b]$.
5. When $A$ multiplies any matrix $B$, it multiplies each column of $B$ separately.   

#### 2.4 Rules for Matrix Operations
1. The $(i, j)$ entry of $AB$ is $(row\ i\ of\ A) \cdot (column\ j\ of B)$.
2. An $m$ by $n$ matrix times an $n$ by $p$ matrix uses $mnp$ separate multiplications.
3. $A(BC) = (AB)C$ 
4. $AB$ is also the sum of these $n$ matrices: (column $j$ of $A$) times (row $j$ of $B$).
5. Block multiplication is allowed when the block shapes match correctly.
6. Block elimination produces the *Schur complement* $D - CA^{-1}B$.  

#### 2.5 Inverse Matrices
1. The inverse matrix gives $AA^{-1} = I$ and $A^{-1}A = I$.
2. $A$ is invertible iff it has $n$ pivots (row exchanges allowed).
3. *Important*. If $Ax = 0$ for a nonzero vector $x$, then $A$ has no inverse.
4. The inverse of $AB$ is the reverse product $B^{-1}A^{-1}$. And $(ABC)^{-1} = C^{-1}B^{-1}A^{-1}$.
5. The **Gauss-Jordan** method solves $AA^{-1} = I$ to find the $n$ columns of $A^{-1}$. The augmented matrix $[A\ I]$ is row-reduced to $[I\ A^{-1}]$.
6. Diagonally dominant matrices are invertible. Each $|a_{ii}|$ dominates its row.

#### 2.6 Elimination = Factorization: $A = LU$
1. Gaussian elimination (with no row exchanges) factors $A$ into $L$ time $U$.
2. The lower triangular $L$ contains the numbers $l_{ij}$ that multiply pivot rows, going from $A$ to $U$. The product $LU$ adds those rows back to recover $A$.
3. On the right side we solve $Lc = b$ (forward) and $Ux = c$ (backward).
4. **Factor**: There are $\frac{1}{3}(n^{3}-n)$ multipilications and subtractions on the left side.
5. **Solve**: There are $n^2$ multiplications and subtractions on the right side.
6. For a band matrix, change the $\frac{1}{3}n^{3}$ to $nw^2$ and change $n^{2}$ to $2wn$.

#### 2.7 Transposes and Permutations
1. The transpose puts the rows of $A$ into the columns of $A^T$. Then $(A^{T})_{ij}= A_{ji}$.
2. The transpose of $AB$ is $B^{T}A^{T}$. The transpose of $A^{-1}$ is the inverse of $A^T$.
3. The dot product is $x\cdot y = x^{T}y$. Then $(Ax)^{T}y$ equals the dot product $x^{T}(A^{T}y)$.
4. When S is symmetric $(S^{T}= S)$, its $LDU$ factorization is symmetric: $S = LDL^T$.
5. A permutation matrix $P$ has a 1 in each row and column, and $P^{T} = P^{-1}$.
6. There are $n!$ permutation matrices of size $n$. *Half even, half odd*.
7. If $A$ is invertible then a permutation $P$ will reorder its rows for $PA = LU$. 

## 3 Vector Spaces and Subspaces
#### 3.1 Spaces of Vectors
1. $R^n$ contains all column vectors with $n$ real components.
2. $M$ (2 by 2 matrices) and $F$ (functions) and $Z$ (zero vector alone) are vector spaces.
3. A subspace containing $v$ and $w$ must contain all their combinations $cv + dw$.
4. The combinations of the columns of $A$ form the **column space** $C(A)$. Then the column space is "spanned" by the columns.
5. $Ax = b$ has a solution exactly when $b$ is in the column space of $A$.
	- $C(A) = $ **all combinations of the columns = all vectors** $Ax$ 

#### 3.2 The Nullspace of A: Solving $Ax = 0$ and $Rx = 0$
1. The nullspace $N(A)$ is a subspace of $R^n$. It contains all solutions to $Ax = 0$.
2. Elimination on $A$ produces a row-reduced $R$ with pivot columns and free columns.
3. Every free column leads to a special solution. That free variable is 1, the others are 0.
4. The *rank* $r$ of $A$ is the number of pivots. All pivots are 1's in $R = rref(A)$.
5. The complete solution to $Ax = 0$ is a combination of the $n - r$ special solutions.
6. $A$ always has a free column if $n > m$, giving a *nonzero solution* to $Ax = 0$.

#### 3.3 The Complete Solution to $Ax = b$
1. The rank $r$ is the number of pivots. The matrix $R$ has $m - r$ zero rows.
2. $Ax = b$ is solvable iff the last $m-r$ equations reduce to $0=0$.
3. One particular solution $x_p$ has all free variables equal to zero.
4. The pivot variables are determined after the free variables are chosen.
5. Full column rank $r=n$ means no free variables: one solution or more.
6. Full row rank $r=m$ means one solution if $m=n$ or infinitely many if $m<n$.

#### 3.4 Independence, Basis and Dimension
1. The columns of $A$ are **independent** if $x = 0$ is the only solution to $Ax=0$.
2. The vectors $v_{1}, ... , v_{r}$ **span** a space if their combinations fill that space.
3. ***A basis consists of linearly independent vectors that span the space.*** Every vector in the space is a *unique* combination of the basis vectors.
4. All bases for a space have the same number of vectors. This number of vectors in a basis is the **dimension** of the space.
5. The pivot columns are one basis for the column space. The dimension is $r$.

#### 3.5 Dimensions of the Four Subspaces
1. The $r$ pivot rows of $R$ are a basis for the row spaces of $R$ and $A$ (same space).
2. The $r$ pivot columns of $A$ (!) are a basis for its column space $C(A)$.
3. The $n-r$ special solutions are a basis for the nullspaces of $A$ and $R$ (same space).
4. If $EA=R$, the last $m-r$ rows of $E$ are a basis for the left nullspace of $A$.

## 4 Orthogonality
#### 4.1 Orthogonality of the Four Subspaces
1. Subspaces $V$ and $W$ are orthogonal if every $v$ in $V$ is orthogonal to every $w$ in $W$.
2. $V$ and $W$ are *orthogonal complements* if $W$ contains **all** vectors perpendicular to $V$ (and vice versa). Inside $R^n$, the dimensions of complements $V$ and $W$ add to $n$.
3. The nullspace $N(A)$ and the row space $C(A^T)$ are orthogonal complements, with dimensions $(n-r)+r=n$. Similarly $N(A^T)$ and $C(A)$ are orthogonal complements with $(m-r)+r=m$.
4. Any $n$ independent vectors in $R^n$ span $R^n$. Any $n$ spanning vectors are independent.

#### 4.2 Projections
1. The projection of $b$ onto the line through $a$ is $p=a\hat{x}=a(a^{T}b/a^{T}a)$
2. The rank one projection matrix $P=aa^{T}/a^{T}a$ multiplies $b$ to produce $p$.
3. Projecting $b$ onto a subspace leaves $e=b-p$ perpendicular to the subspace.
4. When $A$ has full rank $n$, the equation $A^{T}A\hat{x}=A^{T}b$ leads to $\hat{x}$ and $p=A\hat{x}$.
5. The projection matrix $P=A(A^{T}A)^{-1}$ has $P^{T}=P$ and $P^2=P$ and $Pb=p$.  

#### 4.3 Least Squares Approximation
1. The least squares solution $\hat{x}$ minimizes $||Ax-b||^2=x^{T}A^{T}Ax-2x^{T}A^{T}b+b^{T}b$. This is $E$, the sum of squares of the errors in the $m$ equations $(m>n)$.
2. The best $\hat{x}$ comes from the normal equations $A^{T}A\hat{x}= A^Tb$. E is a minimum.
3. To fit $m$ points by a line $b=C+Dt$, the normal equations give $C$ and $D$.
4. The heights of the best line are $p=(p_{1}, ... , p_{m})$. The vertical distances to the data points are the errors $e = (e_{1}, ... , e_{m})$. A key equation is $A^{T}e=0$.
5. If we try to fit $m$ points by a combination of $n<m$ functions, the $m$ equations $Ax=b$ are generally unsolvable. The $n$ equations $A^{T}A\hat{x}= A^Tb$ give the least squares solution -- the combination with the smallest MSE (mean square error).

#### 4.4 Orthonormal Bases and Gram-Schmidt
1. If the orthonormal vectors $q_{1}, ... , q_{n}$ are the columns of $Q$, then $q^{T}_iq_{j}=0$ and $q^{T}_iq_{i}=1$ translate into the matrix multiplication $Q^{T}Q=I$.
2. If $Q$ is square (an **orthogonal matrix**) then $Q^{T}=Q^{-1}$ : ***transpose = inverse***.
3. The length of $Qx$ equals the length of $x$ : $||Qx||=||x||$.
4. The projection onto the column space of $Q$ spanned by the $q's$ is $P=QQ^{T}$.
5. If $Q$ is square then $P=QQ^{T}=I$ and every $b=q_{1}(q_{1}^{T}b)+...+q_{n}(q_{n}^Tb)$.
6. Gram-Schmidt produces orthonormal vectors $q_{1}, q_{2}, q_{3}$ from independent $a, b, c$. In matrix form this is the factorization $A=QR=$ (orthogonal $Q$)(triangular $R$). 

## 5 Determinants
#### 5.1 The Properties of Determinants
1. The determinant is defined by $\det I = 1$, sign reversal, and linearity in each row.
2. After elimination $\det A$ is $\pm$ (product of the pivots).
3. The determinant is zero exactly when A is not invertible.
4. Two remarkable properties are $\det AB=(\det A)(\det B)$ and $\det A^{T}= \det A$.

#### 5.2 Permutations and Cofactors
1. With no row exchanges, $\det A =$ (product of pivots). In the upper left corner of $A$, $\det A_k=$ (product of the first $k$ pivots).
2. Every term in the **big formula**, $\Sigma (\det P)a_{1\alpha}a_{2\beta}...a_{n\omega}$ uses each row and column once. Half of the $n!$ terms have plus signs (when $\det P=+1$) and half have minus signs.
3. The cofactor $C_{ij}$ is $(-1)^{i+j}$ times the smaller determinant that omits row $i$ and column $j$ (because $a_{ij}$ uses that row and column).
4. The determinant is the dot product of any row of $A$ with its row of cofactors. When a row of $A$ has a lot of zeros, we only need a few cofactors.

#### 5.3 Cramer's Rule, Inverses, and Volumes
1. Cramer's Rule solves $Ax=b$ by ratios like $x_{1}=|B_{1}|/|A|=|ba_{2}...a_{n}|/|A|$.
2. When $C$ is the cofactor matrix for $A$, the inverse is $A^{-1}=C^{T}/\det A$.
3. The volume of a box is $|\det A|$, when the box edges are the rows of $A$.
4. Area and volume are needed to change variables in double and triple integrals.
5. In $R^3$, the cross product $u \times v$ is perpendicular to $u$ and $v$. Notice $i \times j=k$.

## 6 Eigenvalues and Eigenvectors
#### 6.1 Introduction to Eigenvalues
1. $Ax=\lambda x$ says that eigenvectors $x$ keep the same direction when multiplied by $A$.
2. $Ax=\lambda x$ also says that $\det(A-I\lambda)=0$. This determines $n$ eigenvalues.
3. The eigenvalues of $A^2$ and $A^{-1}$ are $\lambda^2$ and $\lambda^{-1}$, with the same eigenvectors.
4. The sum of the $\lambda$'s equals the sum down the main diagonal of $A$ (*the trace*). The product of the $\lambda$'s equals the determinant of $A$.
5. Projections $P$, reflections $R$, $90\textdegree$ rotations $Q$ have special eigenvalues $1, 0, -1, i, -i$. Singular matrices have $\lambda=0$. Triangular matrices have $\lambda$'s on their diagonal.
6. *Special properties of a matrix lead to special eigenvalues and eigenvectors*.    

#### 6.2 Diagonalizing a Matrix
1. If $A$ has $n$ independent eigenvectors $x_{1}, ... , x_{n}$, they go into the columns of $X$. 
	- **$A$ is diagonalizable by $X$** : $X^{-1}AX=\Lambda$ and $A=X\Lambda X$  
2. The powers of $A$ are $A^{k}=X\Lambda^{k}X^{-1}$. The eigenvectors in $X$ are unchanged.
3. The eigenvalues of $A^k$ are $(\lambda_{1})^{k}, ... , (\lambda_{n})^{k}$ in the matrix $\Lambda^{k}$.
4. The solution to $u_{k+1}= Au_{k}$ starting from $u_0$ is $u_{k}=A^{k}u_{0}=X\Lambda^{k}X^{-1}u_{0}$:
	- $u_{k}=c_{1}(\lambda_{1})^{k}x_{1}+...+c_{n}(\lambda_{n})^{k}x_{n}$ provided $u_{0}=c_{1}x_{1}+...+c_{n}x_{n}$.
	- That shows Steps 1, 2, 3 ($c$'s from $X^{-1}u_0$, $\lambda^k$ from $\Lambda^k$, and $x$'s from $X$)
5. $A$ is diagonalizable if every eigenvalue has enough eigenvectors $(GM=AM)$.
 
#### 6.4 Symmetric Matrices
1. Every symmetric matrix $S$ has *real eigenvalues and perpendicular eigenvectors*.
2. Diagonalization becomes $S=Q\Lambda Q^{T}$ with an orthogonal eigenvector matrix $Q$.
3. All symmetric matrices are diagonalizable, even with repeated eigenvalues.
4. The signs of the eigenvalues match the signs of the pivots, when $S=S^{T}$.
5. Every square matrix can be "triangularized" by $A=QTQ^{-1}$. If $A=S$ then $T=\Lambda$.

#### 6.5 Positive Definite Matrices
1. Positive definite matrices have positive eigenvalues and positive pivots.
2. A quick test is given by the upper left determinants: $a>0$ and $ac-b^{2}>0$.
3. The graph of the energy $x^{T}Sx$ is then a "bowl" going up from $x=0$:
	- $x^{T}Sx = ax^{2}+2bxy+cy^2$ is positive except at $(x, y)= (0,0)$.
4. $S=A^{T}A$ is automatically positive definite if $A$ has independent columns.
5. The ellipsoid $x^{T}Sx=1$ has its axes along the eignevectors of $S$. Lengths $1/\sqrt\lambda$. 
6. Minimum of $F(x,y)$ if $\frac{\partial F}{\partial x}=\frac{\partial F}{\partial y}=0$ and 2nd derivative matrix is positive definite.   

## 7 The Singular Value Decomposition (SVD)
#### 7.2 Bases and Matrices in the SVD
1. The SVD factors $A$ into $U\Sigma V^{T}$, with $r$ singular values $\sigma_{1}\ge ... \ge \sigma_{r} > 0$. 
2. The numbers $\sigma_{1}^2, ... , \sigma_{r}^2$ are the nonzero eigenvalues of $AA^{T}$ and $A^{T}A$.
3. The orthonormal columns of $U$ and $V$ are eigenvectors of $AA^{T}$ and $A^{T}A$.
4. Those columns hold orthonormal bases for the four fundamental subspaces of $A$.
5. Those bases diagonalize the matrix: $Av_{i}=\sigma_{i}u_{i}$ for $i\le r$. This is $AV=U\Sigma$.
6. $A=\sigma_{1}u_{1}v_{1}^T+...+\sigma_{r}u_{r}v_{r}^T$ and $\sigma_1$ is the maximum of the ratio $||Ax||/||x||$.

#### 7.4 The Geometry of the SVD
1. The ellipse of vectors $Ax$ has axes along the singular vectors $u_{i}$.
2. The matrix norm $||A||=\sigma_{1}$ comes from the vector length: Maximize $||Ax||/||x||$.
3. Invertible matrix = (orthogonal matrix)(positive definite matrix) : $A=QS$.
4. Every $A=U\Sigma V^{T}$ has a pseudoinverse $A^{+}=V\Sigma^{+}U^{T}$ that sends $N(A^{T})$ to $Z$. 

## 8 Linear Transformations
#### 8.1 The Idea of a Linear Transformation
1. A transformation $T$ takes each $v$ in the input space to $T(v)$ in the output space.
2. $T$ is **linear** if $T(v+w)=T(v)+T(w)$ and $T(cv)=cT(v)$ : lines to lines.
3. Combinations to combinations: $T(c_{1}v_{1}+...+c_{n}v_{n})=c_{1}T(v_{1})+...+c_{n}T(v_{n})$.
4. $T=derivative$ and $T^{+}=integral$ are linear. So is $T(v)=Av$ from $R^n$ to $R^m$.

#### 8.2 The Matrix of a Linear Transformation
1. If we know $T(v_{1}), ... , T(v_{n})$ for a basis, linearity will determine all other $T(v)$.
2. Matrix $A_{m\times n}$ represents $T$ in these bases:
	1. Linear transformation $T$
	2. Input basis $v_{1}, ... , v_{n}$
	3. Output basis $w_{1}, ... , w_{m}$
3. The change of basis matrix $B=W^{-1}V=B_{out}^{-1}B_{in}$ represents the identity $T(v)=v$.
4. If $A$ and $B$ represent $T$ and $S$, and the output basis for $S$ is the input basis for $T$, then the matrix $AB$ represents the transformation $T(S(u))$.
5. The best input-output bases are eigenvectors and/or singular vectors of $A$. Then 
	- $B^{-1}AB=\Lambda=eigenvalues$ 
	- $B_{out}^{-1}AB_{in}=\Sigma=singular\ values$.

####  8.3 The Search for a Good Basis
1. A basis is good if its matrix $B$ is well-conditioned. Orthogonal bases are best.
2. Also good if $\Lambda=B^{-1}AB$ is diagonal. But the Jordan form $J$ can be very unstable.
3. The Fourier matrix diagonalizes constant-coefficient periodic equations: perfection.
4. The basis $1, x, x^{2}, ...$ leads to $B^{T}B=$ Hillbert matrix: Terrible for computations.
5. Legendre and Chebyshev polynomials are excellent bases for function space.