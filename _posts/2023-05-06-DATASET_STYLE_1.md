---
title:  "Branch color at clade"
metadate: "hide"
categories: [DATASET_STYLE]
image: "/assets/images/DATASET_STYLE_1.png"
visit: "https://tongzhou2017.github.io/itol.toolkit/articles/DATASET_STYLE.html"
---
## Introduction
The function of the `DATASET_STYLE` template is to adjust the style of branches at any level. It includes two subclasses: branch and label. The function parameter is simple, whereas the input data is more complex. The `DATASET_STYLE` template belongs to the "Style" class (refer to the [Class]() for detail information).

Typically, users define a branch or node style by entering the branch or node name, subclass function name, action location, color, font or line style, and size. The selected branch will be displayed in new style changes specified by the sub function. This function has a high level of integration, and its data parameters are relatively complex, posing a great challenge to users.

## Adjust style
This section uses [dataset 1](https://github.com/TongZhou2017/itol.toolkit/tree/master/inst/extdata/dataset1) as an example to show how to adjust the styles. (refer to the  [Dataset](https://tongzhou2017.github.io/itol.toolkit/articles/Datasets.html) for detail information)

### Load data
The first step is to load the `newick` format tree file `tree_of_itol_templates.tree` and its corresponding metadata `df_frequence`. 

```R
library(itol.toolkit)
tree <- system.file("extdata",
                    "tree_of_itol_templates.tree",
                    package = "itol.toolkit")
data("template_groups")
df_data <- data.frame(id = unique(template_groups$group),
                      data = unique(template_groups$group))
```

We can use the branch subtype function to adjust the color of the entire branch area. In E012, we only used two columns of information to implement the function. For other data, subtype information is passed through the "subtype" parameter, position information is passed by the "position" parameter, line thickness is passed by the "size_factor" parameter. When the line type is not explicitly defined, the default is normal line type. Also, colors are generated from the second column of input data as they are not explicitly specified. If the input data contains all six columns of data, the program will also automatically determine which column is subtype, which is color, and so on. In addition, colors can also be defined through the "color" parameter. Therefore, for various possible situations, the program has automated processing methods, reducing the threshold for users to prepare to input data.

```R
unit_12 <- create_unit(data = df_data, 
                       key = "E012_style_1",
                       type = "DATASET_STYLE", 
                       subtype = "branch",
                       position = "clade",
                       size_factor = 5,
                       tree = tree)
write_unit(unit_12)
```