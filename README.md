_v. 1.8.0_  

`rdid` : Robust difference-in-differences
=========================================

Description
-----------

The `rdid' package helps users to implement the robust difference-in-differences (RDID) framework for both the canonical 2 by 2 DID settings and staggered adoption designs.


Installation
------------

The installation of the package can be done through the `github` package. If you don't have it, execute the following code in Stata.
```
net install github, from("https://haghish.github.io/github/")
```

Once you have it, you can install `rdid` package by running the following code in Stata.
```
github install KyunghoonBan/rdid
```

Commands
--------

### `rdid' and `rdid_dy`

The `rdid` command estimates bounds on the average treatment effect (ATE) in the canonical $2 \times 2$ DID setting where there are two groups (control and treatment) and a single treatment event.
Using a simulated dataset ([sim_rdid.dta](sim_rdid.dta)), we can estimate the RDID bounds and their confidence intervals.
```Stata
. use sim_rdid, clear
. rdid Y, treat(D) post(pos) info(t)

 **** RDID Estimation version 1.8 **** 
Y name: Y
D name: D
no covariates

------------------------------------
           Y: Y |       LB        UB 
----------------+-------------------
           RDID |   9.5525   19.0281 
           CI_1 |   5.8990   21.9975 
           CI_2 |   6.1031   21.7694 
           CI_3 |   5.8990   22.9688 
------------------------------------
* RDID: Point estimates for RDID bounds
* CI_1: Confidence interval for the bounds (Ye et al.)
* CI_2: Confidence interval for the ATT (Ye et al.)
* CI_3: Confidence interval for the bounds (Union Bounds)

```
Note that the outcome variable is `Y`, the treatment indicator is `D`, the post-treatment indicator is `pos`, and the information index is `t` (pre-treatment periods are used as information).

If you have more than 2 time periods after the treatment event, you can estimate RDID separately for each post-treatment period using the same information set with the `rdid_dy` command.
```Stata
. rdid_dy Y, treat(D) post(pos) info(t) t(t)

--------------------------------------------------------
           T: t |  RDID_LB   RDID_UB     CI_LB     CI_UB 
----------------+---------------------------------------
              1 |   1.7421   11.2177   -1.8954   13.8617 
              2 |  17.3629   26.8386   13.2717   29.5650 
--------------------------------------------------------
* Confidence intervals are obtained for the bounds (Ye et al.)
```
Note that the option `t(t)' is used to specify the time index for the post-treatment periods.


Please see [the markdown document](rdid.md) or type the following in Stata for details.
```
help rdid
```


### `rdidstag'

The \texttt{rdidstag} command estimates bounds on the ATT over time for different cohorts in the staggered adoption design.
Using a simulated dataset ([sim_rdidstag.dta](sim_rdidstag.dta)), we can estimate the RDID bounds and their confidence intervals.
```Stata
. use sim_rdidstag, clear
. rdidstag Y, g(G) t(year) post(posttreat) info(year)

 **** RDID Estimation version 1.8 **** 
Y name: Y
G name: G
no covariates
--------------------------------------------------------
       ATT(G/T) |  RDID_LB   RDID_UB   95CI_LB   95CI_UB 
----------------+---------------------------------------
       ATT(1/1) | -18.7809    2.7671  -20.5270    3.8479 
       ATT(1/2) | -11.7097    9.8382  -13.6130   11.1579 
       ATT(1/3) |   0.4795   22.0274   -1.7182   23.7447 
       ATT(1/4) |  17.7957   39.3437   15.2702   41.4645 
       ATT(2/1) | -16.3937    0.9654  -18.3162    2.0562 
       ATT(2/2) | -11.2004    6.1587  -13.0741    7.1611 
       ATT(2/3) |  -0.4110   16.9482   -2.6623   18.5490 
       ATT(2/4) |  15.4757   32.8349   12.9259   34.8338 
       ATT(3/1) | -12.6881    0.2594  -14.3484    1.1674 
       ATT(3/2) |  -9.7081    3.2394  -11.4169    4.2333 
       ATT(3/3) |  -0.4762   12.4714   -2.4427   13.8624 
       ATT(3/4) |  13.6745   26.6221   11.1960   28.6741 
       ATT(4/1) |  -9.2049    0.0052  -10.8883    0.7898 
       ATT(4/2) |  -6.8574    2.3526   -8.6012    3.2546 
       ATT(4/3) |  -3.8843    5.3257   -5.7855    6.4972 
       ATT(4/4) |   7.5646   16.7747    5.2623   18.5234 
--------------------------------------------------------
- Information elements: -4 -3 -2 -1 0
- Post-periods: 1 2 3 4
- Groups: 1 2 3 4
```
Note that the outcome variable is `Y`, the cohort variable is `G`, the time index is `year`, the post-treatment indicator for which ATTs are estimated is `pos`, and the information index is `year` (pre-treatment periods are used as information).

Please see [the markdown document](rdidstag.md) or type the following in Stata for details.
```
help rdidstag
```


Author
------

**Kyunghoon Ban**  
Rochester Institute of Technology  
kban@saunders.rit.edu  
<https://sites.google.com/view/khban>  

**Désiré Kédagni**  
UNC-Chapel Hill  
dkedagni@unc.edu  
<https://sites.google.com/site/desirekedagni/>  


References
----------

Ban, K. and D. Kédagni (2023). Robust Difference-in-Differences Models. [https://arxiv.org/abs/2211.06710](https://arxiv.org/abs/2211.06710/)      
Ban, K. and D. Kédagni (2024). rdid and rdidstag: Stata commands for robust difference-in-differences.


License
-------

MIT
