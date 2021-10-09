# GSE520-PS01 for R
GSE520: Advanced Econometrics I.  Problem Assignment 1 in R

---
title: 'GSE 520: Problem Set #1'
author: 
  - "Student: Erick Bohnenblust"
output: html_document
---

### Question 1

Consider the equation $y = \beta_0 + \beta_1 x_1 + \beta_2 x_2$ 

a. Add an additional variable $x_3$ multiplied by $\beta_3$ to the equation (write the entire expression below).

>**Solution:**  
>$$y = \beta_0 + \beta_1 x_1 + \beta_2 x_2 + \beta_3 x_3$$

b. Change the $\beta$'s in the equation above to $\alpha$'s (write the new expression below).

>**Solution:**  
>$$y = \alpha_0 + \alpha_1 x_1 + \alpha_2 x_2 + \alpha_3 x_3$$

### Question 2

Consider the matrix
\begin{align*} x = \left[
  \begin{matrix}
  3 & 1 & 1 \\
  1 & 2 & -1 \\
  2 & -1 & 4
  \end{matrix} \right]
\end{align*}

a. Write the R code to create this matrix.  Call it `x' and use the command ``print(x)`` to show that you created it correctly.  

**Solution:**  
```{R}
x = matrix(c(3,1,2,1,2,-1,1,-1,4),nrow=3,ncol=3)
print(x)
```

b. What is the inverse of the matrix above?  

**Solution:**  
```{R}
x_inv=solve(x)
print(x_inv)
```

c. Is the inverse of the transpose of this matrix equal to the transpose of the inverse of this matrix?

**Solution:**  

>**Transpose of x**\
```{R}
x_t=t(x)
print(x_t)
```  
>**Inverse of the transpose of x**\  
```{R}
x_t_inv=solve(x_t)
print(x_t_inv)
```  
>**transpose of the inverse of x**\  
```{R}
x_inv_t=t(x_inv)
print(x_inv_t)
```  
>**Therefore, they are equal**.  

d. Prove that the transpose of an inverse is equal to the inverse of the transpose (i.e., $(A^{-1})' = (A')^{-1}$).  You should use the align environment to show each step of your proof.  

>**Solution:**  
>\begin{align*}
>((A)^{-1})' = & (A^{-1})'A'(A')^{-1}\\
>= & (AA^{-1})'(A')^{-1} \\
>= & I'(A')^{-1}\\
>= & (A')^{-1}
>\end{align*}
>
>**$$\therefore (A^{-1})'= (A')^{-1}$$**

### Question 3

Consider the following matrix products,
\begin{align*}
(X'X) = \left[
\begin{matrix}
4 & 46 \\
46 & 534
\end{matrix} \right]
\qquad 

(X'Y)= \left[
\begin{matrix}
12.7 \\
146.4
\end{matrix} \right] 
\end{align*}

Use **R** to calculate the value of $(X'X)^{-1}X'Y$.

**Solution:**  

X = X'X\
Y= X'Y

```{R}
X=matrix(c(4,46,46,534),nrow=2,ncol=2)
print(X)
```

```{R}
Y=matrix(c(12.7,146.4),nrow=2,ncol=1)
print(Y)
```

```{R}
X_inv=solve(X)
print(X_inv)
```

```{R}
M=X_inv%*%Y
print(M)
```

### Question 4

Use the data ``airfare.RData`` to answer the following.  This data contains information on airlines routes in the US from 1997-2000.  In includes information like the average fare of the route and the distance of the route, as well as the fraction of flights on that route concentrated with a single carrier.

```{R}
load("~/A_FALL_21_CLASSES/ECO520_Econometrics_I/Data/Data/airfare.RData")
```

a. What is the minimum flight distance in the data set?

**Solution:** 

```{R}
min(data$dist)
```

b. What is the average fare in the data set?

**Solution:** 

```{R}
mean(data$fare)
```

c. What is the average fare for 1998 in the data set?

**Solution:** 
```{R}
mean(data$fare[data$year==1998])
```
d. Many airline routes are only served by a single carrier, giving them potentially large market power to control prices.  What fraction of the markets in the data set have more than 90% of flights served by a single carrier?

**Solution:** 
```{R}
length(data$concen[data$concen>=.90])/ length(data$concen)
```
>or

```{R}
mean(data$concen>.9)
```
