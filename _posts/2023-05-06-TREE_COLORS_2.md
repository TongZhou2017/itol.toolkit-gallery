---
title:  "Branch color at clade"
metadate: "hide"
categories: [TREE_COLORS]
image: "/assets/images/TREE_COLORS_2.png"
visit: "https://tongzhou2017.github.io/itol.toolkit/articles/TREE_COLORS.html"
---
## Introduction
The `TREE_COLORS` allows you to set the style of branches at any level. It has five attributes: "range", "clade", "branch", "label", and "label_background". While style parameters is simple of `TREE_COLORS`, the data parameters are extremely complex. The `Style` template belongs to the "Tree structure" class (refer to the [Class]() for detail information).

To set the style of a branch or node, users must enter the name of the branch tip or node and the attribute such as color, label, style, and size.The selected branch will then display the new styles as defined by the specified attribute. Although this function provides the most comprehensive templates for modifying tree style, its complexity in data parameters proves to be a great challenge for users.

This section shows how to use itol.toolkit to modify the style. The itol.toolkit significantly reduces the difficulty level for using iTOL by enabling automatic data recognition. Without itol.toolkit, users would have to organize various attribute parameters and their corresponding input data manually. With the itol.toolkit, the entire workflow becomes more cohesive, and users can directly output the template files once they have confirmed which data to use.

## Regular flow
This section uses [dataset 1](https://github.com/TongZhou2017/itol.toolkit/tree/master/inst/extdata/dataset1) as an example to show how to draw the line chart. (refer to the  [Dataset](https://tongzhou2017.github.io/itol.toolkit/articles/Datasets.html) for detail information)

### Load data
The first step is to load the `newick` format tree file `tree_of_itol_templates.tree` and its corresponding metadata `df_frequence`. 

```R
library(itol.toolkit)
tree <- system.file("extdata",
                    "tree_of_itol_templates.tree",
                    package = "itol.toolkit")
hub <- create_hub(tree = tree)
data("template_groups")
```

If the user enters all four columns, the program will figure out which is the subclass and which is the color.

We can use the "clade" attribute to apply color adjustments to all branches contained in a node . Like `unit_7`, we used only 2 columns data  to implement the "branch" attribute in `unit_8`. The attribute are fed to the `subtype` parameter. The line type is defined by the `line_type` parameter, which controls whether the line is a dotted line or not, and here we define the different line types as a set of vectors. The line thickness is defined by the `size_factor` parameter.

In `unit_8`, five discrete colors are generated according to the second column of input data, which has five groups. Colors can also be defined using the color parameter.
```R
df_data <- data.frame(id = unique(template_groups$group), 
                      data = unique(template_groups$group))
unit_8 <- create_unit(data = df_data, 
                      key = "E008_tree_colors_2", 
                      type = "TREE_COLORS", 
                      subtype = "clade", 
                      line_type = c(rep("normal",4),"dashed"),
                      size_factor = 5, 
                      tree = tree)
write_unit(unit_8)
```