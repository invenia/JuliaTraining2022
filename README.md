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



## Other cool libraries / orgs

1. [The Main Julia Language Page](https://julialang.org/)
1. [JuliaGaussianProcesses](https://github.com/JuliaGaussianProcesses/)
1. [JuliaDiff](https://juliadiff.org/)
1. [JuliaML](https://github.com/JuliaML)
1. [Turing](https://turing.ml/stable/)
1. [SciML](https://sciml.ai/)
1. [TestEnv](https://github.com/JuliaTesting/TestEnv.jl)



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
