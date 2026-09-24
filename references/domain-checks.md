# Domain-Specific Checks

Load only the applicable section. These are prompts for risk-based inspection, not mandatory checklists and not substitutes for reading the target paper and code.

## 3D vision and graphics

Check when they can affect the target Claim:

- coordinate-frame names, handedness, and axis order;
- world-to-camera versus camera-to-world transforms;
- row-vector versus column-vector conventions;
- camera intrinsics, image resizing, cropping, and principal-point updates;
- depth, disparity, inverse depth, metric scale, and normalization;
- near/far planes, NDC conventions, and projection matrix layout;
- degrees versus radians and quaternion component order;
- point, voxel, mesh, implicit-field, Gaussian, or latent representation assumptions;
- rasterizer or renderer version and differentiability boundaries;
- visibility, occlusion, background, alpha compositing, and depth sorting;
- mesh winding, face orientation, normals, and texture/color space;
- scene split, pose refinement, and evaluation alignment;
- metric protocol, including scale alignment, ICP, cropping, masking, and LPIPS/SSIM/PSNR implementation.

High-value micro-tests include identity transforms, known camera projections, round-trip coordinate transforms, a single primitive render, and a metric computed on identical inputs.

## 4D and dynamic-scene methods

Additionally check:

- frame ordering, timestamps, frame rate, and time normalization;
- interpolation versus extrapolation split;
- canonical-to-observed versus observed-to-canonical deformation direction;
- deformation composition order and whether motion is absolute or residual;
- camera motion versus scene motion disentanglement;
- temporal windowing, padding, and causal/non-causal access;
- topology changes and visibility across time;
- per-frame, per-sequence, and cross-sequence normalization;
- temporal consistency metrics and whether they reuse frames seen during training.

Useful micro-tests include zero-time or identity-deformation behavior, forward/inverse warp consistency, two-frame ordering swaps, and a short rollout with known motion.

## World models

Check:

- observation, action, reward, termination, and state tokenization;
- action repeat, frame stacking, temporal stride, and context length;
- latent deterministic versus stochastic state and sampling temperature;
- teacher forcing, scheduled sampling, and open-loop versus closed-loop evaluation;
- rollout horizon and error accumulation;
- reset, truncation, terminal-state, and absorbing-state semantics;
- reward scaling, discounting, and value-target construction;
- simulator version, environment wrappers, and sticky/random actions;
- policy used for data collection versus policy used for evaluation;
- imagined-rollout metrics versus downstream control performance;
- leakage from future observations, privileged state, or evaluation trajectories.

High-value micro-tests include one-step transition prediction, deterministic replay under a fixed seed, terminal-transition handling, action perturbation, and short-versus-long rollout error comparison.

## Cross-domain numerical checks

When relevant, inspect:

- units and normalization at every boundary;
- dtype, precision, device, and mixed-precision casts;
- broadcasting and silent shape expansion;
- NaN/Inf generation and clipping;
- reduction dimension and mean-versus-sum behavior;
- batch, sequence, view, point, or time dimension order;
- train/eval mode, dropout, BatchNorm statistics, EMA weights, and gradient disabling;
- random seeds and nondeterministic kernels.

Promote a check to project preflight only after it retires a real risk or prevents a confirmed recurring failure.
