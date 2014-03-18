# NREM-REM Cycle Project Outline
The presentation of two R packages for scored human sleep analysis (first package) and visualization (second package).

## Sleep Cycle Tools
[www.github.com/pmanko/sleep.cycle.tools](www.github.com/pmanko/sleep.cycle.tools)
### Motivation
- The study of human sleep frequently involves analyses across multiple sleep episodes.

- Current metrics for comparing the timing of events across sleep episodes include time since sleep onset, etc. etc.

- These methods do not take into account the underlying structure of each episode...the cyclic nature of sleep. 

- Sleep cycles could be used to "line up" sleep episodes for analysis. However, the definitions and methods for determining sleep cycles using scored sleep data are outdated and not very well defined. Rules for defining sleep cycles work for best for healthy, young sleep.

- We're presenting a tool that is able to utilize different methods for determining NREM and REM sleep cycles and compare their relative effectiveness.

## Raster Plotter 
[www.github.com/pmanko/raster.plotter](www.github.com/pmanko/raster.plotter)

### Motivation
- Displaying complex longitudinal data with the capability of superimposing multiple variables is very useful in visualizing sleep.

- We're presenting a tool that can be used to easily create complex raster plots superimposing multiple data types, ideal for sleep research.

# Previous Work
## Research Project

- We're trying to investigate NREM/REM Cycles
- Do a lit review

- brush up on changepoint analysis
  * Sensitivity analysis
- some possible algorythm features:
  - make prerequesite assumptions?
    * length of rem
    * length of nrem
    * number of allowed cycles
  - rely on collapsing of stages?
    * using stage information might provide more clues about robustness of blocks

## Methods to compare
  - changepoint analysis
  - traditional clustering
  - "smart" clustering


Plotting of Cycle information with other types of information

### STEP 2
What to do with the cycle information?
  - FD interactions with NREM REM cycles

Fast views of sleep episode information. 

Background: lit review
https://sites.google.com/site/changepointanalysis/
http://www.variation.com/cpa/tech/changepoint.html


### The Way To Do It

- Start wrtiting Methods
- Start figures and tables
- Sensitivity and Specificity

- Result
- Discussion


### OUTLINE

#### Methods
1. Accurate interpretation and implementation of (Feinberg and Floyd, 1979), (McNew et al., 1971), (Rechtschaffen and Kales, 1968) methodology for identifying rem and nrem cycles based on scored sleep information.
  - Determining sleep:
    * 15 minute minimum for NREM period
    * REM periods merged if NREM interruption < 15 minutes
    * REM periods have a minimum length > 5 min, except for first one
      ** is this needed? instances where this is not used **
    

2. Extension of existing methodology
  - possibly taking an iterative approach to grouping neighboring stages (as done previously)
  - more flexible by taking into account wake bouts
  - more useful for less regular sleep architecture, as found in older subjects or under forced desynchrony
  - incorporates more recent knowledge about nrem-rem cycles and re-evaluates assumptions made in previous efforts.
    * is there a need to treat first rem episode differently?
    * 15 min limit for NREM was arbitrarily set
  - incorporate more information?
    * scored sleep has nrem 1, 2, 3, rem, wake, and current methods largely group the 3 nrem stages together
    * any way to more intelligently use the available information?
** how do you treat wake? try it both ways, look up how it’s dealt with in literature. does it depend on length of the wake? **

3.    Changepoint Analysis of sleep stage data
  -  A more statistically-based approach at identifying nrem/rem bouts
  -  Multiple R packages exist implementing both parametric and non-parametric methods for this type of analysis
  - Input can be at numerous levels:
    * NREM/REM classification
    * Sleep Stage classification
    * Raw EEG data?
  - Work with Wei to figure out what statistic to use as a basis for this method. ‘cpm’ package allows for relatively easy extension with additional types of statistics, and already supports the most commonly-known parametric and non-parametric ones 
(Student-t, Bartlett, GLR, Fisher’s
Exact Test, Exponential, Mann-Whitney, Mood, Lepage, Kolmogorov-Smirnov, and Cramer-
von-Mises)
  - Supervised vs. Unsupervised results - compare algorithm run under constraints vs. pure change point analysis

**Crucial to comparing these algorithms is the definition of some “golden standard” toward which the methods are striving **
  - multiple “standards” could be defined, each with its own purpose
  - example:
    * # of epochs residing in differently classified bouts, such as rem epochs in nrem bouts

#### Figures and Tables
* Raster Plots with raw sleep stage information and nrem/rem cycle designation depending on methods.
* Sensitivity and Specificity results re: correct classification of individual epochs?
* comparisons of # of cycles, length of cycles, etc.

#### Utilization
  - a wide range of sleep architectures 
    * young, old
    * different levels of sleep deprivation
    * forced desynchrony - different phases
** some methods might be better at dealing with more difficult sleep structure **
** patterns/trends might emerge in distribution/resolution/number/length etc. ** 

#### End Products
  - 2 R Packages
    * raster plotter
    * sleep cycle detection
  - paper on the different cycle detection methods



#### Terminology
* bouts: short homogeneous collections of sleep stages
* blocks: longer groupings of bouts
* cycles: start of a block of one type until start of the next block of same type

#### Some Notes

#### TODO
* look at histograms on REM latency
* create manuscript folder on I drive
* read papers

**how to think about the goal of these algorithms?**
Basically, we want a parsimonious # of accurately labeled blocks. 

We could look at it using information criteria - what fit of parameters are we getting the most info (AIC)

The tradeoff would be between minimizing # of blocks and maximizing the correct classification of bouts in each block.

#### Papers To Read
- Dijk + Czeisler, Neuroscience Letters, 94/95?
- McNew et al, 1971
- How wake is treated in different sleep period/cycle definitions
- Jeanne, Dijk: older people sleep (last or previous PPG)
- People awoken for variable amounts of time (Andrew should send it)
- David Cohen, in phase/ out of phase definitions (Ask Wei)
