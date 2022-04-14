---
title: "3D Neural Scene Representations for Visomotor Control"
layout: post
categories: paper
mathjax: true
baseimg: "/img/neural-scene-rep-nerf-tcn"
---
Paper: [https://arxiv.org/abs/2107.04004](https://arxiv.org/abs/2107.04004)

# Summary
- Learn viewpoint-invariant scene representations with NeRF & TCN
- The learned 3D representations perform well on visuomotor control tasks
- Main selling point: This method can cope with a new viewpoint by incorporating 3D representation!

**In sentences:**
```markdown
3D Neural Scene Representations for Visuomotor Control
A novel approach to represent a 3D scene with NeRF and Time Contrastive loss.
The trained encoder coupled with "auto-decoding trick" is shown to produce representations that generalizes well to unseen viewpoints.
Experiments are performed on water-pouring task where the goal configuration is given by an image from an unseen viewpoint.
```
**Key related works:**  
NeRF, TCN

---
# Main experiment settings
## Tasks
FluidPour
- Pouring water with a robot arm
- 20 cameras are set surrounding the robot
- Goal: reach a goal configuration (specific water-pouring pose)
    - The goal configuration is given as images from (1) a viewpoint during training, (2) interpolated viewpoint between training viewpoints, and (3) an extrapolated viewpoint
They also have FluidShake, RigidStack and RigidDrop.

## Overview
![overview]({{ page.baseimg }}/overview.png){:style="display:block; margin-left:auto; margin-right:auto" }

# Methods
Training objective

$$
L = L_{\text{rec}} + L_{\text{tc}} + L_{\text{dyn}}
$$

- $$L_{\text{dyn}}$$ : L2 loss between two consequtive states given action
- $$L_{\text{tc}}$$ : max-margin loss across time
- $$L_{\text{rec}}$$ : NeRF loss that depends on state representation $$s_t$$

Training procedure:
1. Train $$f_\text{enc}$$ and $$f_\text{dec}$$ together by minimizing $$L_\text{rec}$$ and $$L_\text{tc}$$
2. Fix encoder params, and train the dynamics model $$f_\text{dyn}$$

# A trick: Inference by Optimization (i.e., Auto-decoding)
> Apply the inference-by-optimization (i.e., auto-decoding) framework that backprop through the volumetric renderer and the neural implicit representation into the state estimate.

> This is inspired by the fact that the rendering function, $$f_\text{dec}(x, d, s_t) = (\sigma_t, c_t)$$ is viewpoint equivariant,...

Basically $$f_\text{dec}$$ should generate the same results if we move the camera along with its ray (closer or farther away).
They leverage this and optimized $$L_\text{ad} = \|I_t - \hat{I_t}\|^2$$ to update $$s_t$$.
Note that this only updates $$s_t$$ and the decoder params are fixed during this process.

The resulting state $$s$$ is used as $$s_\text{goal}$$ for planning.

![auto-decoding]({{ page.baseimg }}/auto-decoding.png){:style="display:block; margin-left:auto; margin-right:auto; width: 500px"}

# Not sure
- How does NeRF take an extra state vector in adition to $$(x, y, z, \theta, \phi)$$ ??
- Should read pixel-NeRF stuff
