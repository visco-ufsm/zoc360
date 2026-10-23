# zoc360

Official code for the paper **"Zonal Overfitted Coding for 360° Images"** by Diego R. Chaves, Gabriel S. Baggio, Giovanni Gaiardo and Thiago L.T. da Silveira, accepted at **VCIP 2026**.

This work builds on [MoRIC](https://github.com/eedavidwu/MoRIC) (Li, Wu, Gündüz, NeurIPS 2025), which is itself based on [Cool-Chic](https://github.com/Orange-OpenSource/Cool-Chic). It adapts the codec to 360° images in Equirectangular Projection (ERP), using ERP-aware masks, WS-MSE / WS-PSNR and a combined loss.

## Structure

```
zoc360/
├── train.py                      # Training / encoding entry point
├── run_experiments.sh            # Example launcher
├── lossy_contour_algorithm.py    # Lossy mask contour coding
├── lossless_contour_algorithm.py # Lossless mask contour coding
├── results_logger.py             # CSV logging
├── enc/                          # Cool-Chic derived helpers (loss, coding structure)
├── models/                       # Masked_INR model and candidate training
└── utils/                        # ARM, quantizer, upsampling, WS-PSNR/MSE, BD-rate
```

## Installation

```bash
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
```

## Data

Datasets are **not** included. Place them as expected by `train.py`:

```
dataset/
├── kodak_data_set/   kodimXX/  kodak_mask/  kodak_lossy_mask/
├── clic_data_set/    clicXX/   clic_mask/   clic_lossy_mask/
└── other_data_set/   othimXX/  other_mask/  other_lossy_mask/   # 360° ERP images
```

<!-- TODO: links para download das imagens 360 / máscaras -->

## Usage

```bash
python train.py --type other --mask_type erp --loss_type wsmse \
    --swhdc_tag 1 --erp_padding 1 --lambda_rate_list 0.020 --workdir runs/example
# or
bash run_experiments.sh
```

Compute WS-PSNR between two images:

```bash
python utils/wspsnr_offline.py original.png reconstructed.png
```

## Citation

```bibtex
@inproceedings{chaves2026zoc360,
  title     = {Zonal Overfitted Coding for 360{\textdegree} Images},
  author    = {Chaves, Diego R. and Baggio, Gabriel S. and Gaiardo, Giovanni and da Silveira, Thiago L.T.},
  booktitle = {IEEE International Conference on Visual Communications and Image Processing (VCIP)},
  year      = {2026}
}
```

## License

MIT (see `LICENSE`).
