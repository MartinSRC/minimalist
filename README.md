Graphics with ggplot2
========================================================

At present, ggplot2 cannot be used to create 3D graphs or mosaic plots.
Use I(value) to indicate a specific value. For example size=z makes the size of the plotted points or lines proporational to the values of a variable z. In contrast, size=I(3) sets each point or line to three times the default size.
Here are some examples using automotive data (car mileage, weight, number of gears, number of cylinders, etc.) contained in the mtcars data frame.


```r
# ggplot2 examples
library(ggplot2)

# create factors with value labels
mtcars$gear <- factor(mtcars$gear, levels = c(3, 4, 5), labels = c("3gears", 
    "4gears", "5gears"))
mtcars$am <- factor(mtcars$am, levels = c(0, 1), labels = c("Automatic", "Manual"))
mtcars$cyl <- factor(mtcars$cyl, levels = c(4, 6, 8), labels = c("4cyl", "6cyl", 
    "8cyl"))

# Kernel density plots for mpg grouped by number of gears (indicated by
# color)
qplot(mpg, data = mtcars, geom = "density", fill = gear, alpha = I(0.5), main = "Distribution of Gas Milage", 
    xlab = "Miles Per Gallon", ylab = "Density")
```

![plot of chunk block 1](figure/block_11.png) 

```r

# Scatterplot of mpg vs. hp for each combination of gears and cylinders in
# each facet, transmittion type is represented by shape and color
qplot(hp, mpg, data = mtcars, shape = am, color = am, facets = gear ~ cyl, size = I(3), 
    xlab = "Horsepower", ylab = "Miles per Gallon")
```

![plot of chunk block 1](figure/block_12.png) 

```r

# Separate regressions of mpg on weight for each number of cylinders
qplot(wt, mpg, data = mtcars, geom = c("point", "smooth"), method = "lm", formula = y ~ 
    x, color = cyl, main = "Regression of MPG on Weight", xlab = "Weight", ylab = "Miles per Gallon")
```

![plot of chunk block 1](figure/block_13.png) 

```r

# Boxplots of mpg by number of gears observations (points) are overlayed and
# jittered
qplot(gear, mpg, data = mtcars, geom = c("boxplot", "jitter"), fill = gear, 
    main = "Mileage by Gear Number", xlab = "", ylab = "Miles per Gallon")
```

![plot of chunk block 1](figure/block_14.png) 


# Customizing ggplot2 Graphs
Unlike base R graphs, the ggplot2 graphs are not effected by many of the options set in the par( ) function. They can be modified using the theme() function, and by adding graphic parameters within the qplot() function. For greater control, use ggplot() and other functions provided by the package. Note that ggplot2 functions can be chained with "+" signs to generate the final plot.


```r
library(ggplot2)

p <- qplot(hp, mpg, data = mtcars, shape = am, color = am, facets = gear ~ cyl, 
    main = "Scatterplots of MPG vs. Horsepower", xlab = "Horsepower", ylab = "Miles per Gallon")

# White background and black grid lines
p + theme_bw()
```

![plot of chunk block2](figure/block21.png) 

```r

# Large brown bold italics labels and legend placed at top of plot
p + theme(axis.title = element_text(face = "bold.italic", size = "12", color = "brown"), 
    legend.position = "top")
```

![plot of chunk block2](figure/block22.png) 


