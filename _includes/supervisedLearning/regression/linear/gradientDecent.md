## Gradient Decent

Notes:
- sensitivity of initialization
- may stay at saddle or local minimas
- step size problems
	- too large of a step size increases the time of convergence because may jump back and forth around the minima
	- too small step of a step size increases the time of convergence because the steps towards the minima are too small
	- some ways in practice to improve step size is to:
		- change it linearly by the iteration
		- Newton's method: look at the second derivative to identify the local curvature of the function and decide of how big or small a step to take in a particular direction

### Stochastic / Online Gradient Descent
The classic gradient decent breaks down to taking the sum squared errors of the residual and update based on the weights of each data point.  For stochastic gradient decent we chose a point at random and use that point to update the gradient $$\nabla J$$.  In practice you do some sort of random ordering of the data and go through this ordering sequentially updating the parameter $$\beta$$.  This has the property that on average over the data points the optima $$E[\nabla J_n(\beta)] = \nabla J_n(\beta) = 0$$

Pros:
- Lots of data = many more updates per pass
- computationally faster especially at the beginning where the error is large.  After only a few passes the updates become significant to reduce the error because the decision plane will move closer to the data cluster in space.
Cons:
- no longer strictly "descent" 
	- harder to debug
	- harder to asses convergence
	- stopping condition may be harder to evaluate
Remedy:
- Mini-batch Updates

