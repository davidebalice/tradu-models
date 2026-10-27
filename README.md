# Tradù models

Mobile-optimized ONNX files of **NLLB-200 distilled 600M** (Meta AI), used by the Tradù Android app for fully offline translation.

The files are attached to the [v1 release](https://github.com/davidebalice/tradu-models/releases/tag/v1):

| File | Size |
|---|---|
| nllb-encoder.onnx | 5 MB |
| nllb-encoder.onnx.data | 414 MB |
| nllb-decoder.onnx | 11 MB |
| nllb-decoder.onnx.data | 465 MB |

## What changed from the original

They start from the int8 quantized export by [Xenova/nllb-200-distilled-600M](https://huggingface.co/Xenova/nllb-200-distilled-600M):

- the output head runs `MatMulInteger` on the int8 weights instead of dequantizing the whole 256k×1024 vocabulary matrix at every step (about 5× faster);
- the shared embedding matrix is stored once, pre-transposed, and reused for the embedding lookup;
- weights live in external `.data` files that ONNX Runtime can memory-map instead of copying into RAM.

Same outputs as the original model.

## License and attribution

NLLB-200 is © Meta Platforms, Inc., released under **CC-BY-NC 4.0**: non-commercial use only, with attribution.
These files are a modified version (format conversion and graph optimization only, no retraining).

- Paper: *No Language Left Behind: Scaling Human-Centered Machine Translation*, NLLB Team, 2022
- Original model: https://huggingface.co/facebook/nllb-200-distilled-600M
- License: https://creativecommons.org/licenses/by-nc/4.0/
