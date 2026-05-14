# vjepa-decoder
A generative decoder pipeline for reconstructing V-JEPA 2.1 embeddings back into pixel space using Stable Diffusion 1.5.

## Usage:

- Download the T2I-Adapter weights from huggingface:
```bash 
wget https://huggingface.co/abdullah-hmed/vjepa_21_t2i_adapter_sd15/resolve/main/vjepa_t2i_adapter_sd15_step4550.pt 
```

- Download the RealisticVision Stable Diffusion 1.5 Checkpoint from the URL:

```
https://civitai.com/models/4201/realistic-vision-v60-b1
```

Alternatively, you can also fetch the weights from diffusers.

The official V-JEPA 2.1 codebase has some issues regarding the URL for downloading the model, so we'll do it manually: 
- Download encoder weights: 
```
wget https://dl.fbaipublicfiles.com/vjepa2/vjepa2_1_vitl_dist_vitG_384.pt
```
and place in 
```
C:\Users\<username>\.cache\torch\hub\checkpoints
``` 
or 
```
/root/.cache/torch/hub/checkpoints/
```

Once setup, download the necessary libraries imported in the **t2i_notebook.ipynb** and you should be set. Will work on a inference script in the future. 

## Tips For Better Decoding:


- V-JEPA 2.1 works with square frames, so you can either letterbox the media or center crop. Letterboxing keeps the whole frame but lowers the quality, while center crop omits parts of the frame but retains quality. Take your pick.
- Results can be improved by playing around with the cond_scale, lowering it increases the quality of decoded frame but makes it less faithful.
- Use LCM Scheduler + LCM LoRA with low steps for faster results, or DDIMScheduler with high steps for more detail but slow generation.

## Decoded Examples:

<video src="assets/birb_small.mp4" controls="controls"></video>
<br>
<video src="assets/squirrel_small.mp4" controls="controls"></video>

<hr>
<video src="assets/squirrel_cropped_small.mp4" controls="controls"></video>
<br>Same squirrel video with the center cropping instead of letterboxing