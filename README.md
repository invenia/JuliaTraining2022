# JuliaTraining2022

# Pre-requisites:
1. Install Julia 1.8.1 using https://github.com/JuliaLang/juliaup
    1. Verify that you can run `julia` at your terminal of choice
    1. Have your preferred text editor installed
    1. Really good vscode plugin
    1. Feel free to use vim / sublime / whatever else you prefer



# Data Links

1. [NYC Open Dog Data](https://data.cityofnewyork.us/Health/NYC-Dog-Licensing-Dataset/nu7n-tubp) -- csv at http://tinyurl.com/dogdata2022
1. [OWID Emissions Data](https://github.com/owid/co2-data) -- csv at https://raw.githubusercontent.com/owid/co2-data/master/owid-co2-data.csv


# Useful general packages

## Standard Libraries

1. LinearAlgebra
1. Random
1. Statistics
1. Pkg



## Libraries covered in the workshop

1. [DataFrames](https://github.com/JuliaData/DataFrames.jl)
1. [CSV](https://github.com/JuliaData/CSV.jl)
1. [Plots](https://github.com/JuliaPlots/Plots.jl)
1. [Flux](https://github.com/FluxML/Flux.jl)
1. [MLDataSets](https://github.com/JuliaML/MLDatasets.jl)
1. [StatsBase](https://github.com/JuliaStats/StatsBase.jl)
1. [Distances](https://github.com/JuliaStats/Distances.jl)
1. [StringDistances](https://github.com/matthieugomez/StringDistances.jl)



## Very Popular Libraries (not covered in the workshop)

1. [Revise](https://github.com/timholy/Revise.jl)
1. [IJulia](https://github.com/JuliaLang/IJulia.jl)
1. [Pluto](https://github.com/fonsp/Pluto.jl)
1. [Julia VSCode Plugin](https://code.visualstudio.com/docs/languages/julia) (not actually a Julia package)
1. [BenchmarkTools](https://github.com/JuliaCI/BenchmarkTools.jl)
1. [TestEnv](https://github.com/JuliaTesting/TestEnv.jl)


## Other cool libraries / orgs

1. [The Main Julia Language Page](https://julialang.org/)
1. [JuliaGaussianProcesses](https://github.com/JuliaGaussianProcesses/)
1. [JuliaDiff](https://juliadiff.org/)
1. [JuliaML](https://github.com/JuliaML)
1. [Turing](https://turing.ml/stable/)
1. [SciML](https://sciml.ai/)

# Exercises

## Plotting

### Plotting 1

For the year 2019, make a scatter plot on log-log scale,
where each point is a particular country, 
the x-axis is the emissisions (`total_ghg`), the y-axis is GDP and it is coloured by population.

Tips:
 - you can slice dataframes via `df[df.year .== 2019, :]`
 - the function is `scatter`
 - coloring is with `zcolor` keyword argument

### Plotting 2

Produce a line plot with 1 line per country,
showing how their emmissions (`total_ghg`) have changed over time

For reasability you will likely want to subset to only a few countries of interest.

Tips:
 - line plots use the `plot` function
 - use the `group` keyword argument to group by country to get seperate lines

## Deep Learning

### Deep Learning 1

Use [Flux](https://github.com/FluxML/Flux.jl) to train a conv net to classify MNIST (maybe
don't run on the GPU if you don't have one to hand).

Tips:
 - Use [MLDatasets](https://github.com/JuliaML/MLDatasets.jl) to make getting the data simple
 - Look at the examples in the model zoo if you're stuck


### Deep Learning 2

Julia is a language in which new packages are being developed on a regular basis, so you
might as well get your hands dirty with a library that is a little more rough around the
edges than the ones we've seen so far.
[SimpleChains](https://github.com/PumasAI/SimpleChains.jl) is a new package for training and running smaller neural net architectures
on the CPU.
The performance is really quite impressive.
Use it to train the same model as before on the CPU, but faster.

Tips:
 - There's a nice LeNet example in the docs which you might want to take inspiration from.

## Gaussian Processes

### Gaussian Processes 1

This is quite a low-level exercise, that will get you familiar with some more of the generic ML tools in the ecosystem, in particular generic optimisation packages, algorithmic / automatic differentiation, parameter handling packages, and tools for working with Gaussian processes (GPs).

Obtain the (famous) Mauna Loa CO2 data, [(CSV here)](https://scrippsco2.ucsd.edu/assets/data/atmospheric/stations/in_situ_co2/monthly/monthly_in_situ_co2_mlo.csv)
- plot it
- handle and missing data etc
- fit a GP to it by optimising the negative log marginal likelihood of the kernel parameters of some GP of your choosing

We recommend using the [JuliaGaussianProcesses](https://github.com/JuliaGaussianProcesses) ecosystem -- it's quite low-level, but gives you a lot of flexibility.
You'll need to use AbstractGPs and KernelFunctions for sure.
We recommend using [Zygote.jl](https://github.com/FluxML/Zygote.jl/) to for automatic differentiation.
In order to optimise the kernel parameters, we recommend making use of the BFGS implementation in [Optim.jl](), a generic optimisation package.
You can also use [Optimisers.jl](https://github.com/FluxML/Optimisers.jl) if you prefer to use an optimiser like ADAM.
You'll probably want to use a package like [ParameterHandling](https://github.com/invenia/ParameterHandling.jl/) to make constraining / handling parameters straightforward.

Tips:
 - Consider a model which utilises the sum of a kernel with a period of 1 year, and a kernel with a length scale of roughly 10 years. You can probably keep the period of the periodic kernel fixed, but you'll need to optimise the other parameters to get a good fit.
 - Look at the README of [ParameterHandling.jl](https://github.com/invenia/ParameterHandling.jl) for an example of how to combine the various packages in order to tune the parameters of a GP.
 - If you're stuck, look at the examples / docs in AbstractGPs or [Stheno.jl](https://github.com/JuliaGaussianProcesses/Stheno.jl) where we solve this exact problem.


### Gaussian Processes 2

Utilise [Stheno.jl](https://github.com/JuliaGaussianProcesses/Stheno.jl) to construct an appropriate GP model and decompose the Mauna Loa data into a periodic component and a long-term trend component.

Tips:
 - You can probably just re-express your model from the last exercise in terms of the sum of a couple of GPs
 - If you get really stuck, looks at the examples / docs in [Stheno.jl](https://github.com/JuliaGaussianProcesses/Stheno.jl)
