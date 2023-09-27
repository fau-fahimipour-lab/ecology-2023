# Assignment 3
You may use any software to create your document (e.g., Microsoft Word, Google Docs, LaTeX, Markdown, etc.), but submit your assignment as a PDF. Refer to Assignment 1 if you need a reminder for how to run R code in your web browser. Most questions can be answered correctly in 1, 2, or 3 sentences.

## The Lotka-Volterra Predation System
As we discussed in class, we can use the so-called Lotka-Volterra model to understand the dynamics of predators and prey species. Because we are talking about two species, now our model has two equations --- one for prey and one for predators --- and these equations have different forms because they interact in different (asymmetric) ways. There are four important processes that the predator and prey equations need to capture:

1. The prey species $N$ grows exponentially in the absence of the predator
2. The prey species $N$ has a mortality caused by the predator
3. The predator species $P$ grows by consuming the prey
4. The predator species $P$ has a constant *per capita* mortality rate

Let’s put these elements together into a 2-dimensional dynamical system, where we are tracking both the prey $N$ and predator $P$ population densities over time. Remember, dynamical systems and differential equations are the primary mathematical tools we have to represent *things that change in time*. From populations of predators, to stock markets, to chemical reactions, to the strategies of warring nations, differential equations are how we make sense of *variables*. Often, the ways in which these variables change in time (*i.e.*, the dynamics) depend on certain rules that we represent using *parameters*. The equations we discussed in class are:

$\frac{dN}{dt} = r N - a R P$

$\frac{dP}{dt} = b a R P - m P$

and as you'll recall, whenever you see $\frac{dX}{dt}$ you should think "I am talking about the change in the number of $X$'s over a small change in time $t$" or in other words, the population growth rate.

### Question 1.1
If the predator population goes extinct, what is the equation for the prey population?

### Question 1.2
If the prey population goes extinct, what is the equation for the predator population? How does this differ from the equation for the prey population under the predator extinction condition?

## What do the parameters mean?
Let’s examine the different parameters that we have to consider. Remember, parameters are just placeholders for numbers. Let’s begin by looking at the prey population $N$ because one of the parameters here is already familiar to us. First, we see that the prey population $N$ grows according to a parameter $r$ which, just like before, is the instantaneous rate of growth and has units of 1/**time** or another way to write this is **time**$^{-1}$. The parameter $a$ is new to us, however, and it’s units are not clear to you yet. Let’s examine the units for all of the parameters to see if we can build insight into what a represents. The central rule here is that the units of the left hand side must equal the units of the right hand side. Also it is important to remember that if we add quantities with the same unit, the result will have the same unit... in other words, if $N$ has units of **individuals** and $P$ has units of **individuals**, then $N + P$ has units of **individuals**. However if the terms are multiplied or divided by each other, the units take on the results of those operations. So $N \times P$ has units of **individuals**$^{2}$.

As we observe in the above comparison of *parameter* and *variable* units on both sides of the equation, this new parameter has units of 1/(**time** $\times$ **individuals**) for the units on both sides of the equation to match. And as you should be able to guess given the impact on $\frac{dN}{dt}$ as $a$ is increased or decreased, a larger $a$ means that the growth of the prey is slowed down, and a smaller $a$ means that the growth is increased. The meaning of $a$, which will be more apparent when we examine the equation for predator growth, is the **capture efficiency** of prey by the predator. If a predator is more efficient (higher $a$), it captures more prey individuals per unit time. So the predator is more efficient at extracting prey biomass to create more predator individuals. In other words, there are more captures per prey per unit time (which corresponds to the units for $a$ 1/(**time** $\times$ **individuals**)). Now let’s examine the entire quantity $− a N P$. From this we see that if there are more predators $P$, there is more prey biomass taken away (and the growth of the prey declines), and that this amount scales with the population size of the prey $N$.

So we can learn some things right away by just thinking about these equations and saying (out loud with words) what they represent. Let's keep going. As we discussed in class, the parameter $b$ is often called the **conversion efficiency** and must be a value between 0 and 1. So if I eat a cheesburger and my body assimilated ten percent of those calories to turn into new cells, then my $b = 0.1$. As we can see above, whatever is taken from the prey population by the term $− a N P$ is added to the predator population by $+ b a N P$. If $b$ varies between 0 and 1, we can see that not all biomass taken from the prey population becomes new predator biomass, and this is because much of the potential energy is lost during transfer as heat. In fact, we often assume that $b$ is pretty close to 0 (say 3 percent, 0.03) in most predator-prey interactions, though this number can vary substantially. It is also one of the primary reasons we are more likely to run into herbivores when out for a hike than we are to run into predators!

### Question 2.1
Let’s assume the 'prey' that we are considering is a plant species, and the 'predator' is an herbivore. Would $b$ be expected to by higher or lower relative to $b$ for a carnivore eating an herbivore? Why?

## Dynamics of the Lotka-Volterra model
Now that we have a better understanding of the Lotka-Volterra system and the parameters involved, let’s deploy the same tools that we used to investigate the LV competition system to understand the dynamics here. First, recall the steps we went through in class find the **isoclines** that describe the long-term dynamics:

1. Set the $\frac{d}{dt}$ equations to 0 to solve for the steady state. These will be the equations for the isoclines of the system. Here we will be finding the prey isocline (where $\frac{dN}{dt} = 0$) and the predator isocline (where $\frac{dP}{dt} = 0$).
2. Find the x- and y-intercepts of the prey and predator isoclines so that we can plot them in the phase space where the density of prey, $N$, is on the x-axis and the density of predators, $P$, is on the y-axis.
3. Determine the flow in the 2-dimensional space by solving for prey growth ($\frac{dN}{dt} > 0$), prey decline ($\frac{dN}{dt} <> 0$), predator growth ($\frac{dP}{dt} > 0$), and predator decline ($\frac{dP}{dt} < 0$).
4. From the flow along the $N$ and $P$ axes, find the composite flow (*i.e.*, flow along the diagonal directions). The composite flow will tell us how the population densities of prey $N$ and predator $P$ change over time, as well as the final state of the system.

You should refer to lecture notes and the relevant book section in Ch. 12 to review this if you need.

Below is a code block where the LotkaVolterra predator-prey system is simulated. The main output will be a plot showing the predator $P$ (red) and prey $N$ (blue) isoclines, as well as the starting point and trajectory of the $P$ and $N$ populations over time (green circle and line, respectively). On the top right inset is a smaller plot of the two $P$ and $N$ population sizes visualized in a different way --- plotted over time. Make sure that you understand how the isoclines determine the flow and direct how the combined trajectories of $P$ and $N$ (green) change over time, and how this corresponds to the same model simulation visualized in a different way as population time series (the inset plot).

```r
library(RColorBrewer)
library(deSolve)
pal = brewer.pal(3, 'Set1')
## Define the Rates function
pred.flow = function(r, a, b, m, Pstart, Nstart, tmax){
    yini  = c(P = Pstart,N = Nstart)
    fmap  = function (t, y, parms) {
    with(as.list(y), {
        dP = b*a*y[2]*y[1] - m*y[1]
        dN = r*y[2] - a*y[2]*y[1]
        list(c(dP, dN))
    })}
    times = seq(from = 0, to = tmax, by = 0.1) 
    out   = ode(y = yini, times = times, func = fmap, parms = NULL)
    Ptraj = out[,2];
    Ntraj = out[,3];
    timeline = out[,1];
    Pend = tail(Ptraj, n = 1)
    Nend = tail(Ntraj, n = 1)
    maxtraj = max(c(Ptraj,Ntraj));
    Psize = maxtraj*1.2;
    Nsize = maxtraj*1.2;
    p_isocline = m/(b*a)
    n_isocline = r/a
    par(fig = c(0,1,0,1))
    plot(rep(p_isocline,100),seq(-10,Psize,length.out=100),type='l',lwd=2,col=pal[1],xlim=c(0,500),ylim = c(0,150),xlab='N population',ylab='P population',lty=2)
    lines(seq(-10,Nsize,length.out=100),rep(n_isocline,100),lwd=2,col=pal[2],lty=2)
    points(Nstart,Pstart,pch=16,cex=2,col=pal[3])
    lines(Ntraj,Ptraj,col=pal[3],lwd=2)
    points(Nend,Pend,pch=8,cex=2,col=pal[3])
    legend(0,maxtraj*1.2,c('P isocline','N isocline'),pch=16,col=pal)
    par(fig = c(0.5,1, 0.5, 1), new = T)
    plot(timeline,Ptraj,type='l',col=pal[1],xlab='Time',ylab='Pop. size',lwd=2,ylim=c(0,maxtraj))
    lines(timeline,Ntraj,type='l',col=pal[2],lwd=2)}
## Plug in parameter values and run HERE
pred.flow(r = 0.5, a = 0.01, b = 0.1, m = 0.1, Pstart = 70, Nstart = 100, tmax = 500)
```

### Question 3.1
Suppose the parameter values I gave you in the code block above represent the typical conditions for a predator-prey species pair. Now suppose strange environmental conditions cause the predator **conversion efficiency** to fall by half. Compare the dynamics between the model with $b = 0.1$ to dynamics with $b = 0.05$. Tell me in words what happens to the predator-prey cycle.
