# The implementation of Neural ODE

### 1. From Machine Learning to ODE

Many non-linear problems can be solved using ML. 

The idea of Neural Networks is to learnable matrices of parameters.

The first question someone not familiar with the field might ask is, why are differential equations important in this context? The simple answer is that a differential equation is a way to specify an arbitrary nonlinear transform by mathematically encoding prior structural assumptions.

Let's unpack that statement a bit. There are three common ways to define a nonlinear transform: direct modeling, machine learning, and differential equations. Directly writing down the nonlinear function only works if you know the exact functional form that relates the input to the output. However, in many cases, such exact relations are not known a priori. So how do you do nonlinear modeling if you don't know the nonlinearity?

One way to address this is to use machine learning. In a typical machine learning problem, you are given some input xxx and you want to predict an output yyy. This generation of a prediction yyy from xxx is a machine learning model (let's call it MLMLML). During training, we attempt to adjust the parameters of MLMLML so that it generates accurate predictions. We can then use MLMLML for inference (i.e., produce yyys for novel inputs xxx). This is just a nonlinear transformation y=ML(x)y=ML(x)y=ML(x). The reason MLMLML is interesting is because its form is basic but adapts to the data itself. For example, a simple neural network (in design matrix form) with sigmoid activation functions is simply matrix multiplications followed by application of sigmoid functions. Specifically,

ML(x)=σ(W3⋅σ(W2⋅σ(W1⋅x)))ML(x)=\sigma(W_{3}\cdot\sigma(W_{2}\cdot\sigma(W_{1}\cdot x)))
ML(x)=σ(W 
3
​
 ⋅σ(W 
2
​
 ⋅σ(W 
1
​
 ⋅x)))
is a three-layer deep neural network, where W=(W1,W2,W3)W=(W_1,W_2,W_3)W=(W 
1
​
 ,W 
2
​
 ,W 
3
​
 ) are learnable parameters. You then choose WWW such that ML(x)=yML(x)=yML(x)=y reasonably fits the function you wanted it to fit. The theory and practice of machine learning confirms that this is a good way to learn nonlinearities. For example, the Universal Approximation Theorem states that, for enough layers or enough parameters (i.e. sufficiently large WiW_{i}W 
i
​
  matrices), ML(x)ML(x)ML(x) can approximate any nonlinear function sufficiently close (subject to common constraints).

So great, this always works! But it has some caveats, the main being that it has to learn everything about the nonlinear transform directly from the data. In many cases we do not know the full nonlinear equation, but we may know details about its structure. For example, the nonlinear function could be the population of rabbits in the forest, and we might know that their rate of births is dependent on the current population. Thus instead of starting from nothing, we may want to use this known a priori relation and a set of parameters that defines it. For the rabbits, let's say that we want to learn

rabbits tomorrow=Model(rabbits today).\text{rabbits tomorrow} = \text{Model}(\text{rabbits today}).
rabbits tomorrow=Model(rabbits today).
In this case, we have prior knowledge of the rate of births being dependent on the current population. The way to mathematically state this structural assumption is via a differential equation. Here, what we are saying is that the birth rate of the rabbit population at a given time point increases when we have more rabbits. The simplest way of encoding that is

rabbits′(t)=α⋅rabbits(t)\text{rabbits}'(t) = \alpha\cdot \text{rabbits}(t)
rabbits 
′
 (t)=α⋅rabbits(t)
where α\alphaα is some learnable constant. If you know your calculus, the solution here is exponential growth from the starting point with a growth rate α\alphaα: rabbits(tstart)e(αt)\text{rabbits}(t_\text{start})e^{(\alpha t)}rabbits(t 
start
​
 )e 
(αt)
 . But notice that we didn't need to know the solution to the differential equation to validate the idea: we encoded the structure of the model and mathematics itself then outputs what the solution should be. Because of this, differential equations have been the tool of choice in most science. For example, physical laws tell you how electrical quantities emit forces (Maxwell's Equations). These are essentially equations of how things change and thus "where things will be" is the solution to a differential equation. But in recent decades this application has gone much further, with fields like systems biology learning about cellular interactions by encoding known biological structures and mathematically enumerating our assumptions or in targeted drug dosage through PK/PD modelling in systems pharmacology.

So as our machine learning models grow and are hungry for larger and larger amounts of data, differential equations have become an attractive option for specifying nonlinearities in a learnable (via the parameters) but constrained form. They are essentially a way of incorporating prior domain-specific knowledge of the structural relations between the inputs and outputs. Given this way of looking at the two, both methods trade off advantages and disadvantages, making them complementary tools for modeling. It seems like a clear next step in scientific practice to start putting them together in new and exciting ways!

### 2. From ODE to Neural ODE

### 3. Implementations

### 4. Possible Usecases


### 5. Reference
https://julialang.org/blog/2019/01/fluxdiffeq/

https://alirezaafzalaghaei.github.io/2020/02/26/neural-odes.html

https://msurtsukov.github.io/Neural-ODE/
