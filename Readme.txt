**IMPORTANT: All these notebooks were run on Google's collab (NVIDIA T4 GPU), and hence these are the requirements to run the code.**

Dataset links:
NYU V2 (Training and Evaluation): https://drive.google.com/drive/folders/1-fp_5pm3QY96wZkcAzq_8SPniwnJXwrc?usp=sharing
iBims-1 mat (Evaluation): https://drive.google.com/drive/folders/14x8W2Ui27cCd7vVgu_bB6Z6cAkRljvj-?usp=sharing
iBims-1 png (Evaluation): https://drive.google.com/drive/folders/1JaV3t5xFi2rSjTukdqlwry-ZiZ_jdSby?usp=sharing

**Note: Download the trained weights from the drive link mentioned below and place it in the model_checkpoints folder inside the folder zoedepth**
Trained Weights Link: https://drive.google.com/file/d/18dN7sUuf5UkvRz-juAaL3MKP7XnGu4Kj/view?usp=sharing

Link to entire project materials folder (Datasets, Weights): https://drive.google.com/drive/folders/1dJy_eHf-K8oWxPGv-ndBRpT_7RcxkTjk?usp=sharing

Code References:
ZoeDepth : https://github.com/isl-org/ZoeDepth
UNet: https://github.com/qubvel/segmentation_models.pytorch
NYU V2 Class Mapping: https://github.com/ankurhanda/nyuv2-meta-data/tree/master

Note: For any of the following process, it is mandatory to place the zoedepth folder into the drive, and mount the drive (already in code) since all the following collab codes require the same. The folder model_checkpoints (inside the folder zoedepth) should contain the final best performing weights of the model (can be downloaded from the drive link mentioned above).

Steps to run the code:

- Inference: ZD_Distill_Inference(Image).ipynb and ZD_Distill_Inference(Mat).ipynb
Use ZD_Distill_Inference(Image).ipynb if you have the input images in .png/.jpg format.
Use ZD_Distill_Inference(Mat).ipynb if you have the inputs in .mat format.
Download the trained weights from the drive link mentioned above and place it inside model_checkpoints folder which is in the folder zoedepth.
Before running the code, edit the config_zoedepth.json (which is inside the zoedepth folder) as follows based on your needs:
>save_results : Set true if you want to save the results (img, rel_depth, depth) in png
>save_path : The folder path where you wish to save the results
Inorder to import the input images, specify the root directory in the collab cell, it is expected that the root contains all the input images either in .png/.jpg.
Now, run all the cells till the end for inference.

- Evaluation: ZD_Distill_Eval(Image).ipynb, ZD_Distill_Eval(iBims-1).ipynb, ZD_Distill_Eval(NYU).ipynb
ZD_Distill_Eval(iBims-1).ipynb, ZD_Distill_Eval(NYU).ipynb were used for evaluation of the model on the datasets iBims-1 and NYU respectively.
ZD_Distill_Eval(Image).ipynb can be used for evaluation of inputs which have rgb and depth images in .png format.
Download the trained weights from the drive link mentioned above and place it inside model_checkpoints folder which is in the folder zoedepth.
Before running the code, edit the config_zoedepth.json (which is inside the zoedepth folder) as follows based on your needs:
>save_results : Set true if you want to save the results (img, rel_depth, depth) in png
>save_path : The folder path where you wish to save the results
Inorder to import the input rgb and depth images, specify the root directory in the collab cell, it is expected that the root directory contains 2 subfolders rgb (which contains all input rgb images in .png) and depths (which contains all input depth images in .png with the same filenames as rgb images).
Now, run all the cells till the end for evaluation (metrics).

- Training: ZD_Distill_Train(NYU)
This collab notebook was used for training the model on NYU V2 Dataset. Rename the config_zoedepth(training).json to config_zoedepth.json and use it instead for training. Edit the config as required. The training information is logged onto weights and biases application and hence requires an account for the same. 