---
title: "Ball and Beam Control System"
layout: project-post
# date: 2025-03-05
description: "Design and implementation of a closed-loop feedback controller to autonomously balance a cart on a set of rails using a servo motor and ultrasonic sensor."
tags: [pid, controller, filter]
link: "https://github.com/miron/beam-balance"
image: "/assets/images/ball-beam-balance-setup.jpg"
start_date: 2026-2-21
end_date: 2026-3-21
---

## The Project
The goal was to design, simulate, and implement a control system capable of automatically balancing a rolling cart at a target position along a set of rails. The cart is controlled by tilting the rails with a servo motor, while an ultrasonic sensor continuously measures its position. The challenge: the system is inherently unstable — left uncontrolled, the cart simply rolls off the end.

<img src="/assets/images/ball-beam-annotated.png" width="100%" alt="An annotated image showing the physical system setup.">

## Sensing
The cheap HC-SR04 ultrasonic sensor introduced significant high-frequency noise, which would cause erratic behaviour if left unaddressed. I designed and implemented a second-order digital low-pass filter to smooth the sensor readings, accounting for the small phase delay this introduced downstream in the controller design. The graph below shows how the filter successfully smoothed out high-frequency noise while tracking the underlying position signal.

<img src="/assets/images/ball-beam-filter-graph.png" width="100%" alt="Graph comparing filtered vs. unfiltered ultrasonic sensor response.">
*Raw vs. filtered ultrasonic sensor output.*

## Controller Design
I derived a mathematical model of the system and used it to design a proportional-derivative feedback (PDfb) controller. The PDfb variant was chosen over a standard PD controller to avoid derivative kick, which is an aggressive control spike triggered by sudden changes in the demanded position.

## Simulation and Tuning

The controller was first validated in simulation using Simulink, allowing me to explore the trade-off between response speed and overshoot before touching the hardware. On the real system, I empirically tuned the gains to improve settling time and reduce jitter, with the final controller performing well across both a disturbance test and a position-tracking test.

## Reflections

Real-world factors such as residual sensor noise, friction from slightly misaligned cart wheels, and mechanical compliance, highlighted the gap between a model and reality, and the importance of designing controllers that are robust to it.

See a video of the cart moving between two demanded positions here:

<div style="padding:56.25% 0 0 0;position:relative;"><iframe src="https://player.vimeo.com/video/1200863048?badge=0&amp;autopause=0&amp;player_id=0&amp;app_id=58479&amp;muted=1&amp;loop=1" frameborder="0" allow="autoplay; fullscreen; picture-in-picture; clipboard-write; encrypted-media; web-share" referrerpolicy="strict-origin-when-cross-origin" style="position:absolute;top:0;left:0;width:100%;height:100%;" title="ballbeam-video"></iframe></div><script src="https://player.vimeo.com/api/player.js"></script>

<hr>
<a href="https://www.dubaifuture.ae/hmc" target="_blank"><img src="/assets/images/launcher-HMC-icons.svg" alt="HMC icons for this article." class="HMC-icons"></a>