# Title <!-- Replace 'Title' and this comment with a title or name of your algorithm -->
The Greenness Transformer provides a series of calculations for rgb image data used in monitoring plant growth and health.
A further explanation for the transformer can be found at [this link](https://docs.google.com/document/d/1cAm5w1Bs6dB1SHgf-HVmwwbebLhbZMUvTkXLtas_-xI/edit)

## Authors
Chris Schnaufer

## References
[the link from above](https://docs.google.com/document/d/1cAm5w1Bs6dB1SHgf-HVmwwbebLhbZMUvTkXLtas_-xI/edit) explains the algorithm rationale
and sources

## Transforemer Overview
There are eleven calculations performed within this transformer; explained in more depth in [the link from above](https://docs.google.com/document/d/1cAm5w1Bs6dB1SHgf-HVmwwbebLhbZMUvTkXLtas_-xI/edit).
The algorithms are excess_greenness_index, green_leaf_index, cive, normalized_difference_index, excess_red, exgr, combined_indices_1, combined_indices_2,
 vegetative_index, ngrdi, and percent_green.
 The overall purpose is to provide a way for monitoring plant growth and health and correcting for different lighting conditions

## Quality Statement
The algorithms were tested using sample plot images from [here](https://drive.google.com/file/d/1xWRU0YgK3Y9aUy5TdRxj14gmjLlozGxo/view). The folder was used as the source location for images when
testing

## Additional Information
Further testing on other datasets/images is needed in order to confirm the quality and strength of the algorithms
