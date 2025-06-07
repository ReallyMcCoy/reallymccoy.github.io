---
permalink: /how-to/
author_profile: true
redirect_from:
  - /howto
---

How to...

## Typeset a PhD Dissertation With Published Papers and New Material

Do you want to write a lovely introduction to your PhD dissertation, design a pretty cover, design nice chapter cover pages, and embed the published PDFS from your papers into the file? And do you need it to comply with Harvard's typesetting standards from 2022? You, my friend, are in luck! Check out the slightly modified [Overleaf Template Here](https://github.com/ReallyMcCoy/McCoy_PhD_Dissertation/tree/main). You can see my full typeset dissertation [here](https://www.codymccoy.com/files/McCoy_Dissertation_Illustrations_FINAL.pdf).

<p float="left">
  <img src="/images/Dissertation_cover.jpg" width ="175" />
  <img src="/images/Dissertation_0.jpg" width ="175" /> 
  <img src="/images/Dissertation_5.jpg" width ="175" />
  <img src="/images/Dissertation_5A.jpg" width ="175" />
</p>

## Apply Your Own Theme and Specs Concisely in GGplot

We all have particular, persnickety demands of GGplot. I often want to make many plots where I:
- specify a particular theme (font size 10 everywhere, transparent background to facets, etc)
- define particular specs that I want to include in every plot (e.g., jitter the points with point size 0.25 and alpha = 0.5; set y-axis limits)
- be able to easily change either of the above.

An approach to do so:

```
# set up plotting themes
theme_cody<-theme_classic() +
  theme(
    legend.position="right",
    # legend.title=element_text(size=10),
    # legend.text = element_text(size=10),
    axis.text.x=element_text(size=10),
    axis.text.y=element_text(size=10),
    axis.title.x=element_text(size=10),
    axis.title.y=element_text(size=10),
    strip.text = element_text(size=10),
    strip.background = element_rect(color = "transparent", 
                                    fill = "transparent"))

# make a list of common plot specs
common_layers <- list(
  geom_jitter(alpha=0.75, size=0.25),
  geom_smooth(method="loess", se=FALSE),
  facet_wrap(~Heat_Condition + Light_Condition),
  # coord_cartesian(ylim=c(0.8, 1.25)),
  theme_cody
)

# plot
for (column in variable_columns) {
  p <- ggplot(intsph_plot, aes_string(x = 'day_numeric', 
                                      y = column, 
                                      color = 'species')) +
    common_layers +
    ggtitle(paste(column))
  
  # Save the plot
  ggsave(filename = paste0(rawfigures, "/plot_", column, ".png"), 
         plot = p,
         width=7,height=7)
}

```

## Use FDTD Modeling for Biology

Check out the [primer](https://www.codymccoy.com/files/FDTD_Methods_Primer_MICRON_2021.pdf) that Anna  Shneidman, Alex Davis, Joanna Aizenberg and I wrote on finite-difference time-domain optical simulations for biology. In particular, review the flow chart Anna designed in Figure 2 to help you decide whether to use FDTD (or another method). 

<p float="left">
  <img src="/images/FDTD_flowchart.jpeg" width ="175" />
</p>
