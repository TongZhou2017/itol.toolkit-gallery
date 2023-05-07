---
title:  "Label background color"
metadate: "hide"
categories: [TREE_COLORS]
image: "/assets/images/TREE_COLORS_5.png"
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

We can use the "label_background" attribute to adjust the color scheme of the label background at the branch level. We only used 2 columns of information to show how to implement the "label_background" attribute in `unit_11`. Usually, the background is a uniform color, so the color parameter defines a single color. However, you can set different colors by entering a vector of colors. If no color was set, `itol.toolkit` will automatically set colors based on the data. In practice, it's important to note that backgrounds often don't work the first time you drag them into iTOL, and you need to switch between the ring, rectangle, and unrooted tree types to make them work.

```R
unit_11 <- create_unit(data = template_groups, 
                       key = "E011_tree_colors_5", 
                       type = "TREE_COLORS", 
                       subtype = "label_background",
                       color = "#000000", 
                       tree = tree)
write_unit(unit_11)
```