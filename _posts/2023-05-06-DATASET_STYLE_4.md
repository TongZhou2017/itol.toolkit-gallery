---
title:  "Lable color by node id"
metadate: "hide"
categories: [DATASET_STYLE]
image: "/assets/images/DATASET_STYLE_4.png"
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

We can use the label subtype function to adjust the color of the labels to which the branch area belongs. In E015, we only used 2 columns of information to adjust the style of all labels. For functions that cannot be implemented by E014, it is necessary to define the position as the entire branch in `DATASET_STYLE` in order to use the node id to control large area labels.

```R
unit_15 <- create_unit(data = df_data,
                       key = "E015_style_4",
                       type = "DATASET_STYLE",
                       subtype = "label",
                       position = "clade",
                       size_factor = 1.5,
                       tree = tree)
write_unit(unit_15)
```