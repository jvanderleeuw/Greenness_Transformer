# Greenness Transformer
Provides a variety of calculations using RGB indices in order to monitor crop/plant
growth and health, taking into account variations between lighting and cameras

## Authors
* Clariessa Brown: University of Arizona, Tucson, AZ

* Chris Schnaufer, University of Arizona, Tucson, AZ

* David LeBauer, University of Arizona, Tucson, AZ



## Overview
The Greenness Transformer is meant to provide several calculations on image rgb data in order to get an idea of plant growth and
health. A more in-depth explanation can be found at [this link](https://docs.google.com/document/d/1cAm5w1Bs6dB1SHgf-HVmwwbebLhbZMUvTkXLtas_-xI/edit)

## Algorithm Description
This transformer provides calculations using the red, green, and blue values for pixels in an image ranging from calculating the
percentage of an image which is green to normalized difference calculations and more

## References


### excess_greenness_index: 
* [Sonnentag, O. et. al, 2012](https://www.sciencedirect.com/science/article/pii/S0168192311002851)

    Named ‘2G_RBi’ in Richardson 2007

### green_leaf_index:

### cive: 
* [Kataoka et. al, 2003](https://ieeexplore.ieee.org/document/1225492)

### normalized_difference_index: 
* [Perez et al., 2000](https://www.sciencedirect.com/science/article/pii/S016816999900068X) (links to original paper although equation was slightly modified)

### excess_red:
* [Meyer et al., 1998](https://pdfs.semanticscholar.org/189a/08841373be95d474394a39f2693a7813b2d7.pdf) (links to closely related paper)

### exgr: 
* [Neto et. al, 2004](https://search.proquest.com/docview/305161252?pq-origsite=gscholar)

### combined_indices_1:

* [Guijarro et al., 2011](https://www.sciencedirect.com/science/article/pii/S0168169910001924)

### combined_indices_2: 
* [Guerrerro et al., 2012](https://www.sciencedirect.com/science/article/abs/pii/S0957417412005635)

### vegetative_index: 
* [Hague et al., 2006](https://link.springer.com/article/10.1007/s11119-005-6787-1)

### ngrdi:
* [Hunt et. al, 2005](https://link.springer.com/article/10.1007/s11119-005-2324-5)

### percent_green:
* Richardson et al 2007