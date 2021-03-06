https://scikit-learn.org/stable/modules/gaussian_process.html
The GaussianProcessRegressor implements Gaussian processes (GP) for regression purposes. 
For this, the prior of the GP needs to be specified. 
The prior mean is assumed to be constant and zero (for normalize_y=False) or the training data’s mean (for normalize_y=True). 
The prior’s covariance is specified by passing a kernel object. 
The hyperparameters of the kernel are optimized during fitting of GaussianProcessRegressor by maximizing the log-marginal-likelihood (LML) based on the passed optimizer. 
As the LML may have multiple local optima, the optimizer can be started repeatedly by specifying n_restarts_optimizer. 
The first run is always conducted starting from the initial hyperparameter values of the kernel; 
subsequent runs are conducted from hyperparameter values that have been chosen randomly from the range of allowed values.
If the initial hyperparameters should be kept fixed, None can be passed as optimizer.
The noise level in the targets can be specified by passing it via the parameter alpha, either globally as a scalar or per datapoint.
Note that a moderate noise level can also be helpful for dealing with numeric issues during fitting as it is effectively implemented as Tikhonov regularization, i.e., by adding it to the diagonal of the kernel matrix. An alternative to specifying the noise level explicitly is to include a WhiteKernel component into the kernel, which can estimate the global noise level from the data (see example below).

The implementation is based on Algorithm 2.1 of [RW2006]. In addition to the API of standard scikit-learn estimators, GaussianProcessRegressor:

allows prediction without prior fitting (based on the GP prior)

provides an additional method sample_y(X), which evaluates samples drawn from the GPR (prior or posterior) at given inputs

exposes a method log_marginal_likelihood(theta), which can be used externally for other ways of selecting hyperparameters, e.g., via Markov chain Monte Carlo.
