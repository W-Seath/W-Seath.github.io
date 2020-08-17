## Python constructions of Brownian motion, and a Poisson Process

**Project description:** Python functions for Brownian motion and for the poisson process used in Robert C Merton's jump diffusion model. The exponent used to model asset returns is also included. This is still a work in progress.

### 1. Brownian Motion

Using S<sub>0</sub> to denote the process at time t, with maturity T and the infinitesimal dt. Mu and sigma (&mu; and &sigma;) denote the drift and volatility of the process respectively. By using numpy, the cumulative sumation can be performed incredibly quickly, with almost instantaneous creation of up to 100 processes. 

```python
def BM(S_0,mu,sigma,dt,T):
    
    out = pd.Series(S_0)
    out = out.append(pd.Series(np.cumsum(mu*dt + sigma*np.sqrt(dt)*np.random.normal(0,1,int(T/dt)))),ignore_index=True)
    
    out.index = np.linspace(0,T,int(T/dt + 1))
    
    return out
```
By using numpy, the cumulative sumation can be performed incredibly quickly, with almost instantaneous creation of up to 100 processes.


```python
times = []
for n in range(0,100): 
    tic = time.time()
    for n in range(0,100):
        BM(0,0,0.2,0.001,10)
    toc = time.time()
    times.append(toc-tic)
```
<img src ="images/hundred_brownian_motions_histo.jpeg?raw=true">

