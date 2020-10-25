---
layout: post
title: Preprocessing pipeline for spine surgery
description: Prepares CT images for ultrasound-based image-guided spine surgery. The pipeline provides 1) conversion of preoperative CT from supine to prone position, and 2) extraction of the posterior surface of the vertebra used for image registration.
---

<br/>

This pipeline is intended to work with the **pedicle screw navigation plugin** of IBIS (see [here](https://hgueziri.github.io/projects/2-spine/)). It takes as input supine preoperative CT image and outputs segmented posterior surface of the vertebra.

The processing consists of:
- re-orienting the CT image in prone position
- thresholding the CT image to segment bone tissues
- a fan-shaped ray tracing to extract the posterior-most part of the vertebra

# Method
Once the CT image thresholded, the posterior surface of the vertebra is extracted using a fan-shaped ray-tracing method illustrated in Fig 1. The tracing assumes two origin points at the two extremities of the probe's contact surface (represented by green lines for the right extremity and red lines for the left extremity in the figure). For each ray, the first encountered voxel that belongs to the segmented vertebra is selected to be part of the final surface.

![Fig. 1: Illustration of ray tracing used to extract the posterior surface of the vertebra.]({{site.baseurl}}/assets/images/pipeline/ctraytracing.png)

Parameters:
- the segmentation threshold
  - by default set to 150 Hounsfield unit 
- the distance between the top of the image and the probe's contact surface
  - this represents the antero-posterior distance of the probe, by default set to 5% of the total image height
- the width of the contact surface
  - by default set to 40 mm  

# GitHub

* GitHub page: [https://github.com/hgueziri/SpinePipeline](https://github.com/hgueziri/SpinePipeline)

# TODO

- Implement a more advanced segmentation method for vertebra
  - Although thresholding works fine most of the time, it would be better to have a method that works for pathological and complex cases
- Add parameterization of probe position and dimensions

# References

H.-E. Gueziri, S. Drouin, C. X. B. Yan, D. L. Collins, (2019). [Toward real-time rigid registration of intra-operative ultrasound with preoperative CT images for lumbar spinal fusion surgery](doi: 10.1007/s11548-019-02020-1), International journal of computer assisted radiology and surgery, 14(11), pp.1933–1943.
