---
date:  26 Apr 2020
desc: Uniform distribution - discrete & continuous
imgDesc: 'Image'
name: 'uniform-distribution'
noMainImage: True
title: "Uniform distribution"
altLang: false
---

## Uniform-distribution:
A distribution, where each outcome has probability of equaly, likely chances and they are impossible beyond a range.

## These are discrete uniform distribution:

Consider a draw of card(suit) from a deck of playing card, each suit (clubs, hearts, diamonds & spades) will have a probability of equally, likely chances of 1/4.
The number of values are finite for each suit. We can not get other than 2 to 10, ace, jack, queen & king. 

Consider a roll of a die having 6 faces (1,2,3,4,5 & 6), each face will have a probability of equally, likely chances of 1/6.
The number of values are finite viz., 1,2,3,4,5 & 6. We can not get 1.2, 8, 2.6 or some other value.

The probability mass function(PMF), which gives the probability of x
\begin{equation}
p(x) \geq 0     AND     \sum_{i=1}^n p(x) =1\\\      
p(x) = p(X=x)
\end{equation}

The below images are explaining the PMF of single fair dice & two fair dice.

<div class="mycolumnmd">
<div>
<img src="/education/uniform-distribution/single-fair-dice-pmf.png" alt="alt text" >
</div>
<div>
<img src="/education/uniform-distribution/two-fair-dice-pmf.png" alt="alt text">
</div>
</div>

The cumulative distribution function(CDF), which gives the probability that the variable less than or equal to the value x

\begin{equation}
F(x) = p(X \leq x) = \sum_{x_i \leq x} p(x_i) = p(x_1)+p(x_2)+p(x_3)+...+p(x)
\end{equation}

For any two population values a < b, 

\begin{equation}
p(a \leq X \geq b) = \sum_{a}^b p(x) = F(b) - F(\overline{a})\\\
\text{Where } 
\overline{a} 
\text{ is the preceding value of a, in the sorted population.}
\end{equation}

<div class="mycolumnmd">
<div>
<img src="/education/uniform-distribution/single-fair-dice-cdf.png" alt="alt text" >
</div>
<div>
<img src="/education/uniform-distribution/two-fair-dice-cdf.png" alt="alt text" >
</div>
</div>

## These are continious uniform distribution:

Consider a random variable between any two numbers. It can take any real number with in the range.
The number of values are finited with in the range and they are continuous.



<style>




</style>