# PLIC: Pseudo-Lossy Image Compression

**🚧 Repository Under Construction 🚧**

This repository contains the implementation and experiments for "Quality-Preserving Extreme Image Compression: Using Interpretable Conditioning Inputs with Diffusion Models", a novel compression framework leveraging diffusion models and conditioning inputs to achieve high compression ratios while maintaining strong perceptual similarity and superior image quality.

## Abstract

Diffusion models have revolutionized image synthesis, but their potential for image compression remains underexplored. We introduce PLIC (Pseudo-Lossy Image Compression), a compression framework leveraging diffusion models and conditioning inputs to achieve high compression ratios while maintaining strong perceptual similarity and superior image quality. Unlike traditional neural compressors using abstract latent representations, our approach uses interpretable conditioning inputs (text prompts, canny edges, color palettes) to guide diffusion-based image reconstruction. 

Grounded in rate-distortion-perception theory, PLIC prioritizes minimizing bitrate and distortions over pixel-perfect reconstruction, allowing diffusion models to fill in plausible details during decompression which still results in high perceptual similarity. Evaluating on 490 real-world images scraped from top 1,000 globally visited domains, we demonstrate superior compression ratios (0.004 bits per pixel minimum, 0.197 bits per pixel average) while maintaining excellent image quality (mean BRISQUE=23.36, mean CPBD=0.60) and high perceptual similarity across diverse content types including text, faces, and logos.

📊 **[View Visual Comparison Results](visual_comparision.pdf)** - See how PLIC preserves perceptually important content compared to standard compression methods.

## Method Overview

PLIC leverages three key conditioning inputs for compression:

- **Text Prompts**: CLIP/GPT-generated descriptions capturing semantic content
- **Canny Edges**: Structural boundary information preserving object shapes  
- **Color Palettes**: Dominant color information from downscaled representations
- **Saliency Masks** (optional): Focus regions for enhanced preservation

The framework uses Stable Diffusion 1.5 as the base model, with ControlNet conditioning to guide reconstruction from these interpretable inputs rather than abstract latent codes.

## Repository Structure

- **01_dataset/** – Web scraping pipeline and domain categorization from top 1K websites
- **03_method/** – Batch reconstruction pipeline with mask generation and auxiliary components  
- **04_experiments/** – Core analysis, ablation studies, and figure generation
- **05_evaluation/** – Perceptual similarity metrics (LPIPS, DINO), quality assessment (BRISQUE, CPBD), and baseline comparisons
- **z_archive_exploratory/** – Historical development notebooks and experiments

## Key Results

- **Compression Ratios**: 0.004-0.197 bits per pixel (vs traditional 8-24 bpp)
- **Image Quality**: Mean BRISQUE=23.36, Mean CPBD=0.60
- **Dataset Scale**: 490 real-world images across diverse domains
- **Resolution Range**: 333×687 to 4032×2030 pixels
- **Baselines**: Outperforms neural compressors while maintaining perceptual fidelity

## Quick Start

1. **Dataset Creation**: Run `01_dataset/01_dataset_creation.ipynb` to scrape images from web domains
2. **Domain Categorization**: Execute `01_dataset/02_domain_categorization.ipynb` for content classification
3. **Compression Pipeline**: Use `03_method/01_batch_reconstruction_pipeline.ipynb` for end-to-end compression/reconstruction
4. **Evaluation Suite**: Process through `05_evaluation/` notebooks in sequence for comprehensive metrics

## Technical Implementation

- **Base Model**: Stable Diffusion 1.5 with ControlNet conditioning
- **Conditioning Strategy**: Multi-modal inputs (text + edges + color + saliency)
- **Evaluation Metrics**: LPIPS, DINO similarity, BRISQUE, CPBD, compression ratios
- **Comparison Baselines**: Traditional codecs (JPEG), neural compressors (HiFiC), perceptual optimizers

## Authors

- **Shayan Ali Hassan*** - Lahore University of Management Sciences
- **Danish Humair*** - Lahore University of Management Sciences  
- **Ihsan Ayyub Qazi** - Lahore University of Management Sciences
- **Zafar Ayyub Qazi** - Lahore University of Management Sciences

*These authors contributed equally to this work.

## Research Impact

Our approach demonstrates practical benefits for:
- **Internet Affordability**: Reduced bandwidth requirements without quality loss
- **Archival Storage**: Long-term preservation with minimal storage footprint  
- **Content Distribution**: Scalable delivery for high-resolution media
- **Edge Computing**: Efficient reconstruction on resource-constrained devices
