# Zoe-Distill

## About model:

The model architecture integrates ZoeDepth’s[1] cutting-edge design with an augmented depth-to-segmentation network,
facilitating the transformation of predicted relative depth into segmentation. This innovation fosters a symbiotic relationship
between the segmentation ground truth maps and the depth network during training, enabling seamless knowledge transfer across
tasks.

Moreover, our approach involves a consolidation of semantic classes within the NYU V2[3] dataset, condensing them into
a concise group of 14 classes (using the mapping from [7] for model training. Leveraging the feature maps derived from the
MiDaS[5] core’s decoder, both the segmentation head (U-Net)[6] and the ZoeDepth’s bin module for metric depth are employed.
This strategic fusion introduces additional semantic context from the input image to the MiDaS[5] core, thereby enhancing the
efficacy of the training process.

Notably, this augmentation doesn’t impact inference time as the segmentation component remains inactive during inference.
The visualisation of overall model architecture is shown in Fig 1. The total number of parameters of the model is 105.3M.
Subsequent sections will delve into an in-depth exploration of each core component, elucidating their roles and functionalities
within the model framework.
