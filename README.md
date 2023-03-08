# Equivariant Neural Network Layers
$\mathbf{GL}(m) \times \mathbf{GL}(n)$-equivariant decomposition for linear maps $A \in \mathbf{Hom}(V, W)$ into Schur funcors, as well as the filtration of $K[\mathbf{Hom}(V, W)]$, the coordinate ring, into the associated graded algebra. We would like to potentially use this to help our understanding of equivariant layers in neural networks. 

## Permutation Equivariance in Transformers

This proof is the proof of Claim 1, from Section A of [Are Transformers universal approximators of sequence-to-sequence functions?](https://arxiv.org/abs/1912.10077): 

Suppose $XP$ was given as input, where $P$ is a permutation matrix. First note that 

$$(W^i_KXP)^T(W^i_QXP) = P^T(W^i_KX)^T(W^i_QX)P.$$ 

After the softmax operation, we get 

$$ \sigma[P^T(W^i_KX)^T(W^i_QX)P] = P^T\sigma[(W^i_KX)^T(W^i_QX)]P.$$ 

Then, 

$$\text{Attn}(XP) = XP + \sum_{i=1}^h W^i_O(W^i_V XP) \cdot P^T\sigma[(W^i_KX)^T(W^i_QX)]P $$

$$ = \text{Attn}(X)P,$$

where we used $P^TP = I$. Permutation equivariance of the token-wise feed-forward layer can be shown similarly: 

$$\text{FF}(XP) = \text{Attn}(X)P +W_2\cdot\text{ReLU}(W_1\cdot\text{Attn}(X)P +b_{1,n}1^TP)+b_{2,n}1^TP $$ 
$$ =\text{Attn}(X)P +W_2\cdot\text{ReLU}(W_1\cdot\text{Attn}(X)+b_{1,n}1^T)P +b_{2,n}1^TP $$
$$ =\text{FF}(X)P $$
             
where $\text{ReLU}(XP) = \text{ReLU}(X)P$ was used. This analysis shows that the function class $T_{h,m,r}(\cdot)$ is restricted to permutation equivariant functions.

## Alternate Definition of Attention (and Proof of Equivariance)

$$\text{Attn}(PX) = \text{softmax}\left(\frac{(PX)W_Q((PX)W_K)^T}{\sqrt{d}}\right)(PX)W_V $$

$$= \text{softmax}\left(\frac{(PX)W_Q(W_K^T X^T P^T)}{\sqrt{d}}\right)(PX)W_V $$
                
$$= \text{softmax}\left(\frac{P(XW_QW_K^T)X^TP^T}{\sqrt{d}}\right)(PX)W_V $$
                
$$= P\text{softmax}\left(\frac{XW_QW_K^TX^T}{\sqrt{d}}\right)P^TPXW_V $$
                
$$= P\left(\text{softmax}\left(\frac{XW_Q(XW_K)^T}{\sqrt{d}}\right)XW_V\right) $$
                
$$= P\text{Attn}(X),$$

where we used $P^TP = I$. Proof provided by ChatGPT :)

## Questions About Other Groups

1. What other group equivariance can we build into neural networks? See for example [A General Theory of Equivariant CNNs on Homogeneous Spaces
](https://arxiv.org/abs/1811.02017).
2. How can this be made compatible with transformers? See for example [Group Equivariant Stand-Alone Self-Attention For Vision
](https://arxiv.org/abs/2010.00977).
3. When do we need equivariance? What problems benefit from it? See for example [Geometric Deep Learning: Grids, Groups, Graphs, Geodesics, and Gauges
](https://arxiv.org/abs/2104.13478)
4. How can Group Equivariant Neural Networks be used for NLP? 
5. Are there symmetries in language that we are missing? Invariant theory applications?
6. Is this related to graph grammars and/or the topology of language? See for example [Graph Grammars - http:/ /www.its.caltech.edu](http://www.its.caltech.edu/~matilde/GraphGrammarsLing.pdf)


