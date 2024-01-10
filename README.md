# Project: Accuracy of Student-t Distribution in Estimating Value at Risk (VaR)

## Description
In the complex world of financial markets, effective risk management is crucial. This project focuses on assessing the accuracy of the Student-t distribution in estimating the Value at Risk (VaR), a critical measure of financial risk.

## Problem Statement
The commonly used parametric method for VaR estimation relies on the assumption of normality in returns, which has limitations in capturing the reality of financial markets. How can we enhance VaR accuracy by adopting a more flexible approach, specifically using the Student-t distribution?

## Objectives
- Explore the impact of the Student-t distribution on the accuracy of VaR estimation.
- Highlight advantages compared to the standard parametric method.
- Understand how the Student-t distribution better captures the reality of market movements.
- 
 ## methodology
 ### Definition of Value-at-Risk (VaR) 
The Value at Risk (VaR) is a quantitative measure of financial risk used to estimate the maximum potential loss of an asset portfolio, investment, or open position over a specific period, with a given level of confidence. In other words, VaR estimates the maximum value of a potential loss that should not be exceeded during a specified period, along with the probability of this occurrence.\\

t In addition to this definition, PHILIPPE JORION an expert in financial risk management, proposes a specific formulation:\\
the worst expected loss over a target horizon within a given confidence level.
\\
Following Jorion, we define $W_0$ as the initial investment and $R$ as the expected return over the target horizon. $W_c$ is defined as the lowest portfolio value at the given confidence level $c$, that is, the value of the portfolio should not fall below $W_c$ with probability $c$. VaR is defined as the dollar loss relative to the expected mean value of the portfolio:

\begin{equation}
 \text{VaR} = \mathbb{E}[W] - W_c
\end{equation}

\noindent Defining $R_c$ as the expected return associated with the portfolio value $W_c$, 
\begin{equation}
    W_c = W_0 \cdot (1 + R_c)
\end{equation}
gives us the VaR measured as the loss relative to the mean:
\begin{equation}
     \text{VaR} = -W_0 (R_c -\mu)
\end{equation}
    

   

where $\mu = \frac{W_0-\mathbb{E}[W] }{W_0}$ is the expected return on the portfolio for the target horizon. \\

There are two main types of methods to estimate VaR: parametric methods and non-parametric methods.
\\
### Non-parametric methods
Non-parametric methods for estimating Value at Risk (VaR), such as the historical method and some applications of the Monte Carlo method, provide a flexible approach without the need to specify a particular distribution of returns. The historical method relies simply on ranking past returns, offering ease of application. Its primary advantage lies in its intuitive nature and the fact that it does not require distributional assumptions. However, it may lack precision, especially when market conditions change dramatically.

 The Monte Carlo method, while it can be used in a non-parametric manner, is often implemented with parametric mathematical models to simulate financial returns. The advantage of the Monte Carlo method lies in its flexibility to model complex scenarios, but it can be sensitive to the correct specification of the underlying model. Additionally, it may be computationally and resource-intensive.

 In summary, non-parametric methods offer an alternative to parametric methods, avoiding strict distributional assumptions. However, they may be sensitive to past market conditions, lack precision in unexpected situations, and the Monte Carlo method may require meticulous model management to ensure reliable results, making it more complex.
\subsubsection{Parametric method}
The parametric method for estimating Value at Risk (VaR) relies on the mathematical modeling of financial returns by assuming a specific distribution. This method is a relatively simple approach, but its main drawback lies in the numerous assumptions it makes, particularly the assumption of normality in financial returns. This assumption posits that the fluctuations in returns follow a Gaussian distribution, which can be an overly simplified representation of the reality of financial markets.

When returns do not adhere to a normal distribution, the parametric method can lead to biased VaR estimates. Financial markets often exhibit characteristics of heavy tails, meaning that extreme events occur more frequently than predicted by a normal distribution. By neglecting these heavy tails, the parametric method may underestimate the actual risk, especially during periods of increased volatility or financial crises.

While the parametric method offers simplicity and ease of application, it is crucial to be aware of its limitations. Investors and risk managers should exercise caution when using this approach, recognizing that market conditions may deviate significantly from the assumption of normality.



### Methods to Estimate the Cutoff Return and VaR

In this section, we will model returns and VaR using both the normal distribution and the Student's t-distribution to compare the precision of VaR estimates.\\
First, let's attempt to model the returns.\\
The cuto return is defined as the worst possible realization $R_{c}$ for a confidence
level $c$, and is found from the following integral for the distribution of expected returns $f(r)$, 
\begin{equation}
1-c = \int_{-\infty}^{R_{c}}f(r)dr
\end{equation}

### VaR Estimation Using the Normal Distribution  (Var-n)

if we assume that expected  returns have a normal probability density, this is equivalent  that returns follow a normal distribution with parameters $\mu$ and $\sigma^2$,
$$R\sim N(\mu, \sigma^2)$$
with, 
\begin{itemize}
\item $\mu$: is the expected return on the portfolio for the target horizon
\item $\sigma$: is the standard deviation of the returns 
    
\end{itemize}
So , $$1-c = \int_{-\infty}^{R_{c}} \frac{1}{\sigma\sqrt{2\pi}}e^{-\frac{1}{2}(\frac{r-\mu}{\sigma})^2}dr$$
Let's apply the following change of variable: $$X = \frac{R-\mu}{\sigma},\:\: \text{then,}\:\: X\sim N (0, 1)$$
We finds that, 

$$1-c = \int_{-\infty}^{\frac{R_{c}-\mu}{\sigma}} \frac{1}{\sqrt{2\pi}}e^{-\frac{1}{2}x^2}dx$$
Then, $$1-c = \Psi(\frac{R_{c}-\mu}{\sigma})$$
$\Psi$ is the CDF of normal distribution.\\
Then, $$\Psi^{-1}(1-c) =\frac{R_{c}-\mu}{\sigma} $$
Finally,
$$R_{c} = \Psi^{-1}(1-c)*\sigma+\mu$$

Let's substitute equation $(2.5)$ into equation $(2.3)$ to find an estimator of the VaR, which we will denote as VaR-n.

             $$ VaR-n = -W0*\Psi^{-1}(1-c)*\sigma $$
We are looking for $z_{\alpha}$ in the standard normal distribution table corresponding to the value of $\Psi^{-1}(1-c)$.\\
Then, 

$$VaR-n = -W0*z_{\alpha}*\sigma$$


### VaR Estimation Using Student's t-distribution (VaR-t, VaR-x)
In this section, we will model VaR using the Student's t-distribution. The question that arises is how to choose the degree of freedom for this distribution. We will address this question by estimating the degrees of freedom of the t-distribution using two different methods. This will lead to two distinct VaR models, denoted as VaR-t and VaR-x.\\
\textbf{Definiton 2.1.3 :}
Let $Z$ be a random variable with a centered and reduced normal distribution and let $U$ be a variable independent of $Z$ and distributed according to the $\chi^2$ distribution with $k$ degrees of freedom. By definition, the variable
$$T= \frac{Z}{\sqrt{\frac{U}{n}}},$$
follows Student's distribution with $n$ degrees of freedom.\\
We denote this distribution as $\mathcal{T}(n)$.
\\
#### Propertie 2.1.1:\\
1) The random variable $T\sim \mathcal{T}(n)$ has an even density, making this distribution symmetric,

\[
f_{T}(t) = \frac{1}{\sqrt{n\pi}} \frac{\Gamma\left(\frac{n+1}{2}\right)}{\Gamma\left(\frac{n}{2}\right)} \left(1 + \frac{t^2}{n}\right)^{-\frac{n+1}{2}}, \quad \text{for} \:\:n > 0.
\]



where $\Gamma$ is Euler's Gamma function.

2) $E(T) = 0$ and $Var(T) = \frac{n}{n-2}$ if $n > 2.$


\vspace{0.2cm}
\noindent\textbf{Definiton 2.1.4:}  The probability density function of a non-central Student-t distribution is:
$$f(R) = \frac{1}{\sqrt{\pi\beta n}}\cdot\frac{\Gamma(\frac{n+1}{2})}{\Gamma(\frac{n}{2})}\cdot(1 + \frac{(R-\mu)^2}{n\beta})^{-\frac{1+n}{2}}$$
where \begin{itemize}

\item  $\mu$: denotes a location parameter ( mean of returns) .
\item $\beta$:  represents a dispersion parameter.
\item $n$: is the
degrees of freedom.
\item  $\Gamma$ : is the gamma function.
\end{itemize}


Let's assume that returns follow a non-central Student's t-distribution, with a parameter $\mu$ equal to the mean of the expectded returns and a degree of freedom $n$. 
 
\noindent Let's replace the density of $R$ in Equation $(2.4)$.
\\
We find, $$1-c = \int_{-\infty}^{R_c}\frac{1}{\sqrt{\pi\beta n}}\cdot\frac{\Gamma(\frac{n+1}{2})}{\Gamma(\frac{n}{2})}\cdot\left(1 + \frac{(r-\mu)^2}{n\beta}\right)^{-\frac{1+n}{2}}dr$$
Let's implement the following variable transformation:
$$T = \frac{R-\mu}{\sqrt{\beta}}$$
Thus, the random variable $T$ follows
the Student's t-distribution.
\\
Xe find that,
$$1 -c = \int_{-\infty}^{\frac{R_c -\mu}{\sqrt{\beta}}}\frac{1}{\sqrt{\pi n}}\cdot\frac{\Gamma(\frac{n+1}{2})}{\Gamma(\frac{n}{2})}\cdot\left(1 + \frac{t^2}{n}\right)^{-\frac{1+n}{2}}dt$$
Then, $$1-c =F\left( \frac{R_c -\mu}{\sqrt{\beta}}\right)$$
With $F$ is CDF of student-t distribution. \\
Finally, \begin{equation}
    R_c = F^{-1}(1-c)\sqrt{\beta} + \mu =  F^{-1}(\alpha)\sqrt{\beta} + \mu 
\end{equation}
However, the parameter that remains unknown here is $n$


 To estimate the value of $n$, we will use two methods, which are given as follows:
   



### Var-t
In this model, we opt for the method of moments to express the mean, variance, and excess kurtosis in the following manner: 
\\
 $$\mathbb{E}(R) = \mu$$
    

    $$\sigma^2 = V(R) = \mathbb{E}((R-\mu)^2) = \frac{n\beta}{n -2}$$
  $$K = \frac{6}{n-4}, n>4$$


from this equation we deduce $n$ and $\beta$
\begin{equation}
     n =\frac{6}{K}+4
\end{equation}

\begin{equation}
   \beta = \sigma^2(\frac{3+K}{3+2K}) 
\end{equation}
Substitute the expression for $\beta$ into equation (2.6):
 \begin{equation}
    R_c = t_{\alpha,n} \sigma\sqrt{\frac{3+K}{3+2K}} + \mu
\end{equation}
With $t_{\alpha,n}= F^{-1}(\alpha)$. We find it in the standard Student's t-distribution table with n degrees of freedom.\\
Let's substitute equation $(2.9)$  into equation (2.3) to determine an estimator for the VaR, which we will call VaR-t:

$$VaR-t = -W0*t_{\alpha,n} \sigma\sqrt{\frac{3+K}{3+2K}}$$


### Var-x

The VaR-x  as introduced by Huisman et al. (1998), offers the advantage of incorporating asymmetry by deriving VaR estimates from asset returns on the respective side of the distribution. To assess downside risk, for instance, this approach initiates by determining the tail index of the left tail of the returns distribution. Let \(x(i)\) represent the $i-th$ ascending order statistic of the absolute left-tail returns such that: \(x(i) > x(i-1)\) for \(i = 2, \ldots, N\) N is the size of the sample. Hill (1975) proposed an estimator for the tail index \(\gamma(k)\) as follows:

$$\gamma(k) =\frac{1}{k}\sum_{j=1}^{k}ln(x(N-j+1))-ln(x(N-k))$$
where $k$ denotes as the number of tail observations.\\
The tail index is simple the inverse of
the estimator $\gamma(k)$.\\

\noindent However, the Hill estimator faces a significant bias issue, stemming from the challenge of determining an appropriate value for \( k \) that allows an unbiased estimate of \( \gamma(k) \). This complexity arises because \( k \) plays a crucial role in bias correction for the Hill estimator, and its selection can be intricate.\\

To address this limitation, Huisman et al. (2001) proposed a modified version of the Hill estimator. This modification aims to correct the bias by carefully observing variations in the bias of the Hill estimator as the number of tail observations increases up to a specific threshold . It is noteworthy that  number of tail observations is defined as equal to half of the sample size (i.e., ( Number of tail observations  $= \frac{N}{2} $)), emphasizing its critical role in the bias correction process\cite{6be28a69-688c-3823-bc28-6e115cee45cc}.\\

 The tail index estimator proposed by Huisman and  al. (2001) is:

$$\gamma(k)= \beta_0 + b_1k+\epsilon(k), \:\: k =1,...,N/2,$$


The intercept $\beta_0 $  stands as the optimal estimation for the tail index. \\
\noindent The reciprocal of the estimated $\beta_0$  aligns with the degrees of freedom within the Student-t distribution. (i.e $n = \frac{1}{\beta_0})$
\\
the mean $\mu$ and variance $\sigma^2$ of the yield distribution are estimated.\\
we know that:
$$\sigma^2 = V(R) = \mathbb{E}((R-\mu)^2) = \frac{n\beta}{n -2},\:\:\: n>2$$


then, $$\beta = \frac{\sigma^2}{\frac{n}{n-2}}$$
Substitute the expression for $\beta$ into equation (2.6):
\begin{equation}
    R_{c} = t_{\alpha,n}^{*}\frac{\sigma}{\sqrt{\frac{n}{n-2}}} + \mu\
\end{equation}
 Consult the value \(t_{\alpha,n}^{*}\) from the standard Student t-distribution with appropriate degrees of freedom using tables provided in standard textbooks (see, for example, Bain and Engelhardt 1987) or statistical software.



 The value $R_{c}$ then equals the cuto return needed to calculate the VaR-x
measure for the confidence level $c$. Plugging the expression for $R_{c}$ into equation  (2.3), we
obtain the VaR-x estimate for the VaR as:


$$VaR-x = -W0*t_{\alpha, n}^{*}\frac{\sigma}{\sqrt{\frac{n}{n-2}}}$$
