## 2.2 Opening — The Discounted Cramér-Lundberg Model

We consider an alternative model in which claims are discounted with respect to a rate $\rho \geq 0$ :

$$R_t = u + pt - \sum_{i=1}^{N_t} e^{-\rho(t - \tau_i)} Y_i, \quad t \geq 0$$

where $\tau_i = \inf\{t > 0,\ N_t = i\}$ is the arrival time of the $i$-th claim. The key difference with the classical model is that each claim $Y_i$ is weighted by $e^{-\rho(t-\tau_i)}$, a discount factor that reduces the impact of older claims.

---

### Expected Wealth of the Company

We begin by computing $\mathbb{E}[R_t]$, where $N$ is a homogeneous Poisson process with intensity $\mu$, the $Y_i$ are i.i.d. positive random variables, and $m = \mathbb{E}[Y_1]$.

**Taking the expectation of $R_t$.**
By linearity of expectation,
$$\mathbb{E}[R_t] = u + pt - \mathbb{E}\left[\sum_{i=1}^{N_t} e^{-\rho(t-\tau_i)}Y_i\right].$$
The deterministic terms are straightforward; the whole difficulty lies in computing the last term.

**Separating the claims from the arrival times.**
Since the $Y_i$ are independent of the Poisson process and all share the same mean $m$, we can factor the expectation :
$$\mathbb{E}\left[\sum_{i=1}^{N_t} e^{-\rho(t-\tau_i)}Y_i\right] = m\,\mathbb{E}\left[\sum_{i=1}^{N_t} e^{-\rho(t-\tau_i)}\right].$$
This is the same idea as in the classical model — replace each random claim by its mean — except that here each claim is additionally weighted by its discount factor.

**Conditioning on the number of claims.**
Since $N_t$ is itself random, we condition on $N_t = n$ :
$$\mathbb{E}\left[\sum_{i=1}^{N_t} e^{-\rho(t-\tau_i)}\right] = \sum_{n=0}^{\infty} \mathbb{E}\left[\sum_{i=1}^{n} e^{-\rho(t-\tau_i)} \,\middle|\, N_t=n\right]\mathbb{P}(N_t=n).$$
A classical result on Poisson processes states that, given $N_t = n$, the arrival times $\tau_1, \dots, \tau_n$ are distributed as the order statistics of $n$ i.i.d. uniform random variables on $[0, t]$. In other words, knowing that exactly $n$ claims occurred before $t$, their arrival times are spread uniformly over $[0, t]$.

**Computing the conditional expectation.**
Using this uniform distribution, and denoting $U \sim \mathcal{U}([0,t])$,
$$\mathbb{E}\left[\sum_{i=1}^{n} e^{-\rho(t-\tau_i)} \,\middle|\, N_t=n\right] = n\,\mathbb{E}\left[e^{-\rho(t-U)}\right] = \frac{n}{t}\int_0^t e^{-\rho(t-s)}\,ds.$$

**Removing the conditioning.**
Plugging back into the sum and factoring out the integral,
$$\mathbb{E}\left[\sum_{i=1}^{N_t} e^{-\rho(t-\tau_i)}\right] = \left(\frac{1}{t}\int_0^t e^{-\rho(t-s)}\,ds\right) \sum_{n=0}^{\infty} n\,\mathbb{P}(N_t=n) = \left(\frac{1}{t}\int_0^t e^{-\rho(t-s)}\,ds\right)\mathbb{E}[N_t].$$
Since $N_t \sim \mathcal{P}(\mu t)$, we have $\mathbb{E}[N_t] = \mu t$, and therefore
$$\mathbb{E}\left[\sum_{i=1}^{N_t} e^{-\rho(t-\tau_i)}\right] = \mu \int_0^t e^{-\rho(t-s)}\,ds.$$

**Closed-form result.**
Collecting everything and computing the integral via the substitution $u = t - s$,
$$\mathbb{E}[R_t] = u + pt - \mu m \int_0^t e^{-\rho(t-s)}\,ds = \boxed{u + pt - \frac{\mu m}{\rho}\left(1 - e^{-\rho t}\right)} \quad (\rho > 0).$$
When $\rho = 0$, the discount factor is trivially 1 and one recovers the classical result $\mathbb{E}[R_t] = u + pt - \mu m t$, consistent with the fact that the discounted model is a generalization of the classical one.

---

### The Safety Loading Condition

We now determine the critical premium rate $p^*$ below which the company's expected wealth can become negative.

**Convexity of the expected wealth.**
We differentiate $t \mapsto \mathbb{E}[R_t]$ :
$$\frac{d}{dt}\mathbb{E}[R_t] = p - \mu m\, e^{-\rho t}.$$
The second derivative is
$$\frac{d^2}{dt^2}\mathbb{E}[R_t] = \mu m \rho\, e^{-\rho t} > 0 \quad \text{for all } t \geq 0,$$
so $t \mapsto \mathbb{E}[R_t]$ is **strictly convex**, and any critical point is necessarily a global minimum.

**Case $p \geq \mu m$.**
The first derivative is non-negative for all $t \geq 0$, so $\mathbb{E}[R_t]$ is non-decreasing. Since $\mathbb{E}[R_0] = u \geq 0$, we conclude that $\mathbb{E}[R_t] \geq u \geq 0$ for all $t$.

**Case $p < \mu m$.**
The first derivative vanishes at
$$t^* = \frac{1}{\rho}\ln\!\left(\frac{\mu m}{p}\right) > 0,$$
which is, by convexity, the unique global minimum. Substituting $e^{-\rho t^*} = \frac{p}{\mu m}$, the minimum value is
$$\mathbb{E}[R_{t^*}] = u + \frac{p}{\rho}\ln\!\left(\frac{\mu m}{p}\right) - \frac{\mu m - p}{\rho}.$$
We now show that the second and third terms combine to a strictly negative quantity. Setting $x = \frac{\mu m}{p} > 1$, this reduces to proving that $\ln(x) < x - 1$ for all $x > 1$. Define $g(x) = x - 1 - \ln(x)$. Then $g(1) = 0$ and $g'(x) = 1 - \frac{1}{x} > 0$ for $x > 1$, so $g$ is strictly increasing on $[1, +\infty)$, which gives $g(x) > 0$ for all $x > 1$, i.e. $\ln(x) < x - 1$. Therefore $\mathbb{E}[R_{t^*}] < u$, and in particular $\mathbb{E}[R_{t^*}] < 0$ when $u = 0$.

**Conclusion.**
The condition $\mathbb{E}[R_t] > 0$ for all $t \geq 0$ is guaranteed if and only if $p > \mu m$, regardless of the initial capital $u$. The critical premium rate is therefore

$$\boxed{p^* = \mu m = \frac{\mu}{\beta}.}$$

This threshold is **identical** to that of the classical model, which can be confirmed by letting $\rho \to 0$ : using $e^{-\rho t} \approx 1 - \rho t$, we get $\frac{\mu m}{\rho}(1 - e^{-\rho t}) \to \mu m t$, recovering $p^* = \mu m$.

**A key qualitative difference.**
Although the critical threshold is the same, the behaviour of the model below $p^*$ differs fundamentally from the classical case. In the classical model, $\mathbb{E}[R_t] \to -\infty$ when $p < p^*$. In the discounted model, the total discounted claims are bounded :
$$\frac{\mu m}{\rho}(1 - e^{-\rho t}) \xrightarrow[t \to \infty]{} \frac{\mu m}{\rho} < +\infty,$$
so $\mathbb{E}[R_t] \to +\infty$ regardless of $p$. The financial risk is therefore **concentrated in the short term**, making the discounted model structurally more favourable for the insurer over long time horizons.