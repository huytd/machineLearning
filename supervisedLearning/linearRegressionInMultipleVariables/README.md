Linear Regression In Multiple Variables
=======================================

+ Linear Regression in multiple variables with training set
    - Multiple features/variables
        + n = number of features
        + x^(i) = input (features) of ith training example
        + (x_j)^(i) = value of feature j in ith training example
        + h(x) = theta_0 + theta_1 * x_1 + theta_2 * x_2 + ...
        theta_n * x_n
        + if x_0 = 1, then vector x = [x_0; x_1; ... x_n]
        + and vector theta = [theta_0; theta_1; ... theta_n]
        + COOL THING: we can rewrite h(x) = theta^T * x where T is transpose
        + Remember that GRADIENT DESCENT = algorithm that lets us find a minimal theta(a n+1 dimentional vector)
        + J(theta) = (1/2m)(Sum from i = 1 to m of (h(x^(i))-y^(i))^2 )
    - Feature Scaling = technique for making gradient descent work better = make sure features are on a similar scale
        + For example, if x_1 has a range of values from 0 - 2000 and x_2 has a range of values from 0 - 5
        inverse both values so x_1 = 1/(x_1) and x_2 = 1/(x_2) making both features take on a range of values from
        0 < x_i < 1. Your goal is to get every feature approximately in the range -1 < x_i < 1.
    - Mean normalization = technique for making gradient descent work better = replace x_i with x_i - mu_i to make
    features have approximately zero mean (Do NOT apply to x_0 = 1).
        + new x_i = (x_i - mu_i)/s_i where mu_i is the average value of x_i in training set and s_i is the range of the training set of is the standard deviation of the training set.
    - Picking the Learning Rate Problem:
       + if alpha is too small, there will be a slow convergence. Solution = picker larger alpha.
       + if alpha is too large, J(theta) may not decrease during each iteration of gradient decent and will not converge. Solution = picker smaller alpha.
    - Polynomial Regressioin
       + if your traning data is not lineary distributed you may consider making your h_theta(x) function quadratic or cubic. This can be done even if you only have one feature. For example:
       + you currently have h_theta(x) = theta_0 + theta_1 * x_1 but your data isn't LINEAR
       + so rewrite as h_theta(x) = theta_0 + theta_1 * x_1 + theta_2 * (x_1)^2 giving you are quadratic function
    - Normal Equation = method to solve for theta at once instead of iteratively with gradient descent
       + To understand the reason behind this method first image you have a quadratic equation of the form
       J(theta) = a*theta^2 + b*theta + c
       + to find the value of theta that will give you the smallest value of J(theta) you would take the derivative of J(theta), set the derivative to 0, and then solve for theta.
       + This is the exact same that will be done for the cost function J(theta_0, theta_1, ..., theta_m) instead of J(theta)
       + where theta = (X^T * X)^-1 * X^T * y and can be coded as ```pinv(X' * X) * X' * y```
    - When to use Normal Equation vs. Gradient Descent
       + m = # of training examples and n = # of features
       + Gradient Descent
           - Pros:
              + works well even when n is large
           - Cons:
              + need to choose alpha
              + needs many iterations
       + Normal Equation
           - Pros:
              + no need to choose alpha
              + don't need to iterate
           - Cons:
              + slow if n is very large because we need to compute (X^T * X)^-1 which will take O(n^3) time. If n > 10^4 then you should use gradient instead.
              + does not work for logistic regression