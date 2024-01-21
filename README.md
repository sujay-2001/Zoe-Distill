# Zoe-Distill

## About model:
![Model Archiecture](Model.png)

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

## About ZoeDepth:
ZoeDepth[1], a state-of-the-art (SOTA) model, comprises essential components: the MiDaS[5] Core, responsible for extracting
feature maps and predicting relative depth maps; a metric bins module, predicting bin centers corresponding to each pixel in the
depth map; and a metric depth head module, utilizing log softmax probabilities from the bin centers to derive the final metric
depth values for individual pixels. These pixel-wise probabilities serve as weightings for the predicted bin centers, contributing
to the model’s depth estimation process.

##  Segmentation Cross-Talk Distillation:
![Cross-Talk Distillation](Cross_Talk_Distillation.png)

The feature outputs from the encoder-decoder network, scaled at different levels (1/32, 1/16, 1/8, 1/4, 1/2), serve as input
features for the UNet[6] Decoder. The decoder network (expansive path) takes the feature map from the lower layer, up-converts
it, crops and concatenates it with the encoder data of the same level, and then performs two 3×3 convolution layers followed by
ReLU activation 1. We use UNet[6] encoder with 5 decoder layers. This decoder, encompassing approximately 3M parameters,
generates the final logits for segmentation output. Upon computing the loss, Softmax is applied to derive class probabilities. The
training involves feeding the decoder with inputs associated with 14 distinct classes. The following diagram as shown in Fig 2
illustrates the distillation task while training.


