## Python constructions of Brownian motion, and a Poisson Process

**Project description:** The aim of this mini-project is to develop efficient python functions for Brownian motion and for the poisson process used in Robert C Merton's jump diffusion model. Utilising mostly numpy and pandas libraries, with the output being a pandas series object. Both the fineness of the infinitesimal approximation and the length of the process are taken as inputs, to allow a user to balance efficiency and accuracy depending on their needs (this page is still a work in progress). 

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
<img src ="images/basic stochastic constructions/hundred brownian motions histo.png?raw=true">

Initially, through a typo, I created a brownian-like object with the omission of the np.sqrt(dt) factor, leading to an object where the standard deviation of the process is correlated, and indeed dependent on, the number of points used to approximate the process, as shown in the code and diagram below:

```python
fig,ax = plt.subplots(1,1,figsize=(12,8))
dic = {}

for n in range(1,1000):
    point = np.std(BM(0,n/1000,10))
    dic[n]=point
    
    ax.scatter(n,point,alpha=0.7)
ser = pd.Series(dic)
    
slope, intercept, r_value, p_value, std_err = stats.linregress(ser.index,ser)

x = np.linspace(0,1000,1001)
y = slope*x + intercept
ax.plot(x,y,label='Linear Regression Line',lw=5,color='k')
ax.set_title('Standard Deviation of object vs sampling rate')

print('Slope: '+str(slope))
print('R-Value: '+str(r_value))
plt.xlabel('sample mesh size e-03')
plt.ylabel('Standard Deviation')
ax.legend(loc=0)
```
The above code provides the below plot, with the R value in this case 0.6218, and that is a fairly typical value from running a couple of informal tests.

<img src ="images/basic stochastic constructions/failed brownian.png?raw=true">

Although I am sure that there is no real use for such a construction, it is intersting to take note of it, and it lends insight into the nature of the discretisation for the 'real' Brownian motion.

When putting the correct Brownian motion throught this standard deviation test, it is reassuring to see that the fineness of the discretiastion does not yield such a patter, with R values restign around the ~0.05 range.


<img src ="images/basic stochastic constructions/brownian motion.png?raw=true">
