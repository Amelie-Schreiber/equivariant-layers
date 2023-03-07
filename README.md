# equivariant-basis
$\mathbf{GL}(m) \times \mathbf{GL}(n)$-equivariant decomposition for linear maps $A \in \mathbf{Hom}(V, W)$ into Schur funcors, as well as the filtration of $K[\mathbf{Hom}(V, W)]$, the coordinate ring, into the associated graded algebra. We would like to potentially use this to help our understanding of equivariant layers in neural networks. 

Suppose $XP$ was given as input, where $P$ is a permutation matrix. First note that $(W^i_KXP)^T(W^i_QXP) = P^T(W^i_KX)^T(W^i_QX)P$. After the softmax operation, we get $\sigma[P^T(W^i_KX)^T(W^i_QX)P] = P^T\sigma[(W^i_KX)^T(W^i_QX)]P$. Then, $\text{Attn}(XP) = XP + \sum_{i=1}^h W^i_O(W^i_V XP) \cdot P^T\sigma[(W^i_KX)^T(W^i_QX)]P = \text{Attn}(X)P$, where we used $P^TP = I$.

Permutation equivariance of the token-wise feed-forward layer can be shown similarly: 

\begin{align}
\text{FF}(XP) &= \text{Attn}(X)P +W_2\cdot\text{ReLU}(W_1\cdot\text{Attn}(X)P +b_{1,n}1^TP)+b_{2,n}1^TP \\  
               & =\text{Attn}(X)P +W_2\cdot\text{ReLU}(W_1\cdot\text{Attn}(X)+b_{1,n}1^T)P +b_{2,n}1^TP \\
               &= \text{FF}(X)P
\end{align}              

where $\text{ReLU}(XP) = \text{ReLU}(X)P$ was used. This analysis shows that the function class $T_{h,m,r}(\cdot)$ is restricted to permutation equivariant functions.
