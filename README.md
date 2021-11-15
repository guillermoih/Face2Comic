
# Face2Comic

Use pixel2style2pixel for generating comic images from faces photos.



## Content

- **pixel2style2pixel**: Clone of the pSp StyleGAN project
- **pretrained_models**: Folder for the weights of pretrained StyleGAN and IR-SE50. The IR-SE50 is used in our ID loss during pSp training.
- **Notebook_Face2Comic**: Colab Notebook for download the original pSp repository and the comic dataset for training.
## Required changes

You need to define the paths of your data source, in the /pixel2style2pixel/configs/paths_config.py file.

Define the location of the pretrained models and both the source and target dataset.

***IMPORTANT***

Download the [FFHQ StyleGAN weights](https://drive.google.com/file/d/1EM87UquaoQmk17Q8d5kYIAHqu0dkYqdT/view) and [IR-SE50 Model](https://drive.google.com/file/d/1KW7bjndL3QG3sxBbZxreGHigcCCpsDgn/view) inside the /pretrained_models folder
## Deployment

To train the model execute the following command

```bash
python scripts/train.py \
--dataset_type=face2comic \
--exp_dir={Log output path} \
--workers=8 \
--batch_size={Adapt to the processing power} \
--test_batch_size=8 \
--test_workers=8 \
--val_interval=2500 \
--save_interval=5000 \
--encoder_type=GradualStyleEncoder \
--start_from_latent_avg \
--lpips_lambda=0.8 \
--l2_lambda=1 \
--id_lambda=1 \
--w_norm_lambda=0.025 \
```

For more training options, check /pixel2style2pixel/options folder.

If you wish to resume from a specific checkpoint (e.g. a pretrained pSp model), you may do so using --checkpoint_path.
## Acknowledgements

 - [Original pSp StyleGAN repository](https://github.com/eladrich/pixel2style2pixel)