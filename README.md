# IMLE-GAN: Implicit Maximum Likelihood Estimation with GANs

This repository contains an implementation of IMLE-GAN applied to the **Stacked MNIST** dataset. The model is evaluated in terms of **mode coverage** and **KL divergence**, and compared against a StyleGAN baseline.

---

## Introduction
In Generative Adversarial Networks, mode collapse refers to a phenomenon where the generator produces a limited variety of outputs, failing to capture the full diversity of the target distribution. This leads to a bias in the model, often underrepresenting minority classes. Mode collapse can severely affect the quality of generated samples, especially when the goal is to model complex and varied data distributions. IMLE-GAN combines the strengths of Implicit Maximum Likelihood Estimation (IMLE) with adversarial training to better cover the data distribution and tackle this shortcoming of GANs. This project demonstrates its effectiveness on the Stacked MNIST dataset, which is a challenging benchmark for generative models.

---

## Stacked MNIST Dataset

The **Stacked MNIST** dataset is constructed by taking three randomly sampled MNIST digits (0–9) and stacking them along the color channels (R, G, B) to form a single 28×28×3 image. This yields up to 1,000 possible modes (10³ combinations).

- **Creation Process**  
  1. Sample three independent MNIST digits with replacement.  
  2. Assign each digit image to one of the RGB channels.  
  3. Stack channels to form a colored 28×28 image.  

- **Why Stacked MNIST?**  
  - Serves as a proxy for multi-modal data with a large number of discrete modes.  
  - Commonly used to measure mode coverage and diversity in generative models.

---

## Model Architecture

- **Generator**  
  - Input: 256‑dimensional noise vector  
  - 4 transposed‑convolutional layers with batch norm + ReLU  
  - Output: 28×28×3 image with Tanh activation  

- **Discriminator**  
  - 4 fully conected layers  + LeakyReLU  
  - Final dense layer outputs real/fake score  

- **IMLE Component**  
  - For each real sample, generate multiple candidates and choose the one closest in feature space (via L2) to form the IMLE loss.  
  - Combined with the standard GAN adversarial loss.


---

## Evaluation 
- This implementation achieved 95.7% mode coverage (957/1000) on Stacked MNIST as compared to StyleGan2 (94% mode coverage). 

---

## Sample Outputs

Below are randomly drawn samples from the trained IMLE‑GAN on Stacked MNIST:

![IMLE-GAN Samples](sample_imle_gan.png)


---

## Future Work

- **Real-World Datasets:** Apply to diverse multi-modal datasets (e.g., CELEB-A, CIFAR-10, ImageNet subsets).  
- **Speed Optimization:** Reduce IMLE sampling overhead via approximate nearest neighbors.
---


