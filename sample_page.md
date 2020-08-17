## Python constructions of Brownian motion, and a Poisson Process

**Project description:** Python functions for Brownian motion and for the poisson process used in Robert C Merton's jump diffusion model. The exponent used to model asset returns is also included. This is still a work in progress.

### 1. Brownian Motion

Using $S_0$ to denote the process at time $t$, wiht as By using numpy, the cumulative sumation can be performed incredibly quickly, with almost instantaneous  

```python
def BM(S_0,mu,sigma,dt,T):
    
    out = pd.Series(S_0)
    out = out.append(pd.Series(np.cumsum(mu*dt + sigma*np.sqrt(dt)*np.random.normal(0,1,int(T/dt)))),ignore_index=True)
    
    out.index = np.linspace(0,T,int(T/dt + 1))
    
    return out
```

### 2. Assess assumptions on which statistical inference will be based

```javascript
if (isAwesome){
  return true
}
```

### 3. Support the selection of appropriate statistical tools and techniques

<img src="images/dummy_thumbnail.jpg?raw=true"/>

### 4. Provide a basis for further data collection through surveys or experiments

Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo. 

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).
