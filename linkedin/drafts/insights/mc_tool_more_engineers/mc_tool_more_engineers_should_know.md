# Monte Carlo Simulation: A Tool More Engineers Should Know About

I spent more than two decades working in engineering before I really encountered Monte Carlo simulation.

It wasn't something I remember learning in engineering school, and it wasn't a tool I regularly encountered while designing water and wastewater infrastructure.

I discovered it while expanding my knowledge of data analytics and statistics.

And once I understood what it was, my first thought was:

**Why don't more engineers know about this?**

Despite the somewhat unusual name, Monte Carlo simulation isn't an AI technique or some new development in analytics. It's a well-established numerical method for analyzing uncertainty.

The basic idea is surprisingly simple.

In engineering, we often perform calculations using a set of assumed inputs.

A design flow might be 4.0 MGD.

A construction project might be estimated at $5 million.

An asset might have an expected service life of 50 years.

Those values are useful, and sometimes necessary, for performing calculations and making decisions.

But the real world rarely gives us perfectly fixed numbers.

Future demand may be higher or lower than projected. Construction costs fluctuate. Equipment performance changes over time. Assets deteriorate at different rates. Field conditions introduce uncertainty that wasn't apparent during design.

Traditional engineering calculations often ask:

**What happens if these assumptions are correct?**

Monte Carlo simulation allows us to ask a slightly different question:

**What range of outcomes could occur given the uncertainty in those assumptions?**

## From One Calculation to Thousands

Monte Carlo simulation works by allowing uncertain inputs to vary within defined probability distributions and then repeatedly performing the calculation.

Not once.

Potentially thousands or tens of thousands of times.

Each simulation represents one possible combination of conditions.

Imagine estimating the cost of an infrastructure project.

Instead of assuming every quantity, material price, labor cost, and contingency will occur exactly as estimated, we can represent some of those inputs as ranges of possible values.

A computer can then randomly sample from those ranges and calculate the project cost thousands of times.

Instead of receiving a single answer such as:

**Estimated project cost: $5.0 million**

we might end up with information such as:

**80% of simulated project costs fall between $4.5 million and $5.8 million.**

Or:

**There is a 24% probability that the project cost will exceed $5.5 million.**

That doesn't necessarily make the underlying prediction more certain.

It makes the **uncertainty more visible**.

And that can be extremely valuable when making engineering decisions.

## Where Could Engineers Use It?

The same concept can be applied to many of the uncertainties engineers deal with every day.

Monte Carlo simulation can help evaluate uncertainty associated with:

* Future water demand
* Construction costs
* Infrastructure deterioration
* Asset service life
* Equipment reliability
* Failure risk
* Energy consumption
* Population growth
* Capital improvement planning

The specific application changes, but the underlying idea remains the same.

Rather than pretending every input is known with certainty, we acknowledge that some variables are uncertain and evaluate how that uncertainty affects the possible outcomes.

## A Different Way of Thinking About Engineering Calculations

For me, this is what makes Monte Carlo simulation particularly interesting.

Engineering calculations traditionally produce an answer.

Monte Carlo simulation produces a **distribution of possible answers**.

That shift can change how we think about risk.

Instead of asking only:

**What is the expected outcome?**

We can also ask:

**How likely are we to exceed a critical threshold?**

**What does the worst reasonable case look like?**

**How much variability should we expect?**

**Which assumptions have the greatest influence on the result?**

Those questions can provide valuable context when evaluating infrastructure investments, reliability, risk, and long-term planning.

## It Doesn't Replace Engineering Judgment

Monte Carlo simulation doesn't tell an engineer what decision to make.

And a simulation is only as meaningful as the assumptions, data, and probability distributions behind it.

If those assumptions don't reasonably represent the system being analyzed, running the model 100,000 times doesn't magically make the answer correct.

Computers remain remarkably efficient at producing bad answers very quickly when we give them bad assumptions.

The engineer still has to understand the system, evaluate the inputs, interpret the results, and determine what level of risk is acceptable.

Monte Carlo simulation simply gives us another way to understand the uncertainty surrounding those decisions.

And understanding uncertainty is an important part of engineering judgment.

## Next: Putting It Into Practice

I'm currently working through an applied Monte Carlo simulation using Python to better understand the method beyond the theory.

In an upcoming edition of *Engineering Judgment*, I'll move from the concept to the application and show what a Monte Carlo simulation actually looks like in an engineering problem.

We'll look at how uncertain inputs can be modeled, how thousands of possible outcomes can be simulated, and, most importantly, how those results can help support an engineering decision.

Because the goal isn't to eliminate uncertainty.

It's to understand it well enough to make better decisions.

**Engineering begins with calculations.**
**Infrastructure analytics powers better decisions.**
