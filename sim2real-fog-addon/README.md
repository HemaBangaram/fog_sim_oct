# Sim2Real Fog Add-on (Physics-Guided Sim2Real Diffusion)

Fog counterpart of the rain add-on. DreamBooth-fine-tuned Stable Diffusion v1.5 learns the
`<fog_sim>` concept from CARLA fog images; at test time a real foggy frame is translated to the
CARLA-fog style (Real2Sim) via img2img + IP-Adapter Plus.

## Layout
```
training/
  training_fog_sim.ipynb        DreamBooth fine-tuning
  dataset_fog_sim/              <- put CARLA fog TRAINING images here (5-20 images)
testing/
  testing_fog_real2sim.ipynb    inference (real fog -> sim style)
  evaluation.ipynb              CLIP-DS, cosine, LPIPS, Gram style difference
  input_fog_real/               <- put real foggy TEST images here
  style_fog_sim/                <- put ONE CARLA fog style reference here
  test_vid/                     (optional) test videos
fog_kaggle_run.ipynb            end-to-end runner for Kaggle (GPU)
```

## Run order
1. Add images to `training/dataset_fog_sim/`, `testing/input_fog_real/`, `testing/style_fog_sim/`.
2. Push to your GitHub repo `sim2real-fog-addon` (or edit the clone URL in `fog_kaggle_run.ipynb`).
3. Open `fog_kaggle_run.ipynb` on Kaggle (GPU) -> Run All.
   Order: train -> inference -> evaluation -> zip results.

Training outputs `checkpoint_fog_sim/` and `model_fog_sim/` (under `training/`);
inference writes to `testing/output_fog_real2sim/`.
