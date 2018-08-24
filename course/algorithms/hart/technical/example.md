---
title: Example Page
template: LeafPage
---

# Example of branch creation

Consider a tree that tries to determine if a number is prime. The sample has been picked (with replacement) from a large database of integers and the attributes shown are those that have been picked (without replacement) from the set of attributes in the integer database.

# TABLE OF INPUTS GOES HERE

## Formulae

$$\text{Entropy}(S)=-p\_\oplus\log\_2(p\_\oplus)-p\_\ominus\log\_2(p\_\ominus)$$

$$\text{Gain}(S,A)=\text{Entropy}(S)-\sum\_{v\in\text{values}(A)}\left(\frac{|S\_v|}{|S|}\centerdot\text{Entropy}(S\_v)\right)$$

## Creating the branch

$S=\\{1,2,2,4,7,9,9,9,13,16,17\\}$. The set of attributes $\mathbb{A}=\\{\text{Even?,}\leq8\text{?,}=9?\\}$. The attributes $A\in\mathbb{A}$ are all booleans so $A=\\{0,1\\}$. Denote $\text{Even?}\equiv\mathbb{E}$, $\leq8?\equiv\mathbb{L}$ and $=9?\equiv\mathbb{N}$.

*These sets needn't all be booleans. An attribute could be, for example, "Is the number $0\leq n\leq6$ or $6<n\leq 10$  or not?"*

### Initial Entropy

$p\_\oplus=\frac{5}{11}$ (there are $5$ primes and $11$ total numbers) and $p\_\ominus=\frac{6}{11}$ so the initial entropy is

$$\text{Entropy}(S)=-\frac{5}{11}\log_2\left(\frac{5}{11}\right)-\frac{6}{11}\log_2\left(\frac{6}{11}\right)\approx0.994$$

This is almost as entropic as it can be. To calculate the gain, take all the atributes $A\in\mathbb{A}$ and calculate their individual gains. Using $\mathbb{E}=\\{0,1\\}$ as an example

$$\text{Gain}(S,\mathbb{E})=\text{Entropy}(S)-\underbrace{\frac{4}{11}\cdot\text{Entropy}(S\_1)}\_{\text{Relative entropy of the even numbers}}-\underbrace{\frac{7}{11}\cdot\text{Entropy}(S\_0)}\_{\text{Relative entropy of the odd numbers}}$$

The entropies of the even number and odd numbers are calculated the same way as the entropy of $S$, but using only the subsets $S_i\subseteq S$ for $k\in\\{0,1\\}$.

$$\text{Entropy}(S_1)=-\frac{2}{4}\log_2\left(\frac{2}{4}\right)-\frac{2}{4}\log_2\left(\frac{2}{4}\right)=1$$

$$\text{Entropy}(S_0)=-\frac{3}{7}\log_2\left(\frac{3}{7}\right)-\frac{4}{7}\log_2\left(\frac{4}{7}\right)\approx0.985$$

So $\text{Gain}(S,\mathbb{E})\approx0.994-\frac{4}{11}\cdot1-\frac{7}{11}\cdot0.985\approx0.00355$

Similar calculations are done for $\mathbb{L}$ and $\mathbb{N}$.

$$\text{Gain}(S,\mathbb{L})\approx0.0519$$

$$\text{Gain}(S,\mathbb{N})\approx0.0275$$

$\mathbb{L}$ has the highest gain, so that is the way in which this branch of the overall tree will sort the numbers.

If all possible branches created *reduce* the entropy of your data $\left(\text{Gain}<0\right)$ then you stop branching and that node becomes a leaf. Use the most common output of your data to decide what the leaf categorises your data as. The final tree using these inputs and data is shown below:

![Example Tree](http://cueimps.soc.srcf.net/course/media/calliope/finalgraph.png)