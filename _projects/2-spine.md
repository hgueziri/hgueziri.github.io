---
layout: post
title: Ultrasound-guided spinal navigation
description: This project aims at investigating the feasibility of intra-operative ultrasound (iUS) guidance for spinal fusion surgery. We address the problem of patient-to-preoperative CT image alignment during open spine surgery. The suftware is open-source and freely available as a plugin feature of the IBIS neuronavigation software.
---

( Work in progress! )


Spinal fusion surgery is a common procedure to treat spinal instability when medication and physical therapy fail. During the last two decades, the number of annual spinal fusion procedures has known a significant increase, with over 413,000 interventions reported in the United States. The surgery consists in rigidly fusing multiple vertebrae using rods and bone grafts to help stabilize the spinal column.  The rods are fixed to each vertebra using screws implanted within the vertebral pedicles. 

In open surgery, the posterior part of the vertebra is exposed and the surgeon uses image-guided surgery (IGS) to align the screw trajectory through unexposed anatomy. The current IGS procedure is based on intra-operative 2D fluoroscopy or 3D computed tomography (CT) imaging, which increases operating time, interrupts the surgical workflow and exposes the patient and the operating room personnel to harmful radiations. **In this research, we investigate a radiation-free alternative using intra-operative ultrasound (iUS) imaging for spinal navigation**. The objectives are : 
* to address the problem of patient-to-preoperative image alignment during spine surgery;
* to build an open-source software that provides basic fonctionality features for pedicle screw navigation;
* to evaluate the solution in a clinical environment.

Reference papers:

H.-E. Gueziri, S. Drouin, C. X. B. Yan, D. L. Collins, (2019). [Toward real-time rigid registration of intra-operative ultrasound with preoperative CT images for lumbar spinal fusion surgery](doi: 10.1007/s11548-019-02020-1), International journal of computer assisted radiology and surgery, 14(11), pp.1933–1943.

# Demo

<center>
<div class="embed-responsive embed-responsive-16by9">
    <video width="500" height="375" controls="true" class="embed-responsive-item">
      <source src="{{site.baseurl}}/assets/videos/spineVideo.mp4" type="video/mp4" />
    </video>
</div>
</center>

# Description

The solution was developped as part of the [Intraoperative Brain Imaging System (IBIS)]() navigation platform. IBIS is a freely available platform that provides common functionalities used in IGS. It also allows rapid integration of new functionalities as plugins for specific applications. The current version of the *Pedicle Screw Navigation Plugin* provides: i) fast rigid registration of preoperative CT images to iUS images acquired during open surgery; and 2) multiplanar pedicle screw navigation views.

![Fig. 2: System architecture of the CT-to-iUS rigid registration framework. Doted boxes indicate the intra-operative procedure required to be achieved by the surgeon.]({{site.baseurl}}/assets/images/spine/pediclescrewnav-software.png)

The source code will be made available soon at [https://github.com/IbisNeuronav/Ibis](https://github.com/IbisNeuronav/Ibis).

## CT-to-iUS Registration

An overview of our registration framework is shown in Fig. 2. 
The preoperative stage involves two steps: 
* extract the posterior surface of the vertebra in CT images; and
* extract CT anatomy orientation points.
During the surgery, five intra-operative steps are performed: 
* extract probe’s trajectory points;
* reconstruct the iUS volume from iUS acquisition slices;
* estimate the initial alignment using the iUS scan trajectory and the CT anatomy points; and
* perform a multi-metric registration optimizing *gradient orientation alignment* and *mean of iUS intensities passing through CT vertebra surfaces*.

![Fig. 3: Flowchart of the registration method.]({{site.baseurl}}/assets/images/spine/pediclescrewnav-registration.png)

Three metrics were implemented for optimization during image registration:
* Gradient orientation alignment;
* Mean of iUS intensities passing thourgh CT vertebra surfaces; and
* A linear combination of both metrics.

Validation on a procine cadaver with six vertebral levels: T15 and L1-L6

Metric 			| TRE (mm) 	| Success rate (%) 	| Time (s)
------------------------- | ----------------- | ----------------------- | -----------
Gradient (G) 		| 1.20 		| 85.14 			| 5.57
Intensity (I) 		|1.50 		| 71.43 			| 5.25
Combination (G+I) | 1.47 		| 100 			| 6.62

## Visualization

We use pointer navigation (similar to a pedicle probe) to visualize the trajectory of the screw. A multiplanar slicing is used to obtain Axial and Sagittal views reformatted so that the view planes have the same orientation as the pointer. Figure 4 shows an example of the pedicle screw navigation window. The red line represents the instrument, and a screw cross-section is shown in green.

![Fig. 4: Pedicle screw navigation views.]({{site.baseurl}}/assets/images/spine/navigation.png)

## Source code and binaries

Source: [https://github.com/IbisNeuronav/Ibis](https://github.com/IbisNeuronav/Ibis)

Binaries: TBA
