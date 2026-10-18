# Steam Deck FSR 4.1.1b

## Exact and Lossy builds

Close the game, install OptiScaler if needed, then select **Steam Deck FSR 4 build**
in Basic settings (also available in Quick Access). The selector installs the
chosen DLL and enables the INT8 configuration described below. Options include
the original **4.1.1b**, **iGPU Exact**, and **iGPU Lossy**. The iGPU variants are
pinned to [release dll-2026-10-15](https://github.com/zgauthier2000/fsr4-shader-performance-overrides/releases/tag/dll-2026-10-15).
They use the handheld/iGPU archive, not the desktop GPU archive. The first
download is about 51 MiB; verified DLLs are cached per build for later use.

Exact aims to preserve AMD's image. Lossy is experimental and reduces neural
network work on selected frames, trading image quality for speed. It can soften
motion, introduce ghosting, and alternate frame times. Read the upstream
[quality comparison](https://github.com/zgauthier2000/fsr4-shader-performance-overrides/blob/main/docs/exact-vs-lossy.md)
and the archive's `lossy/WARNING.txt`. Do not use these builds in online games or
games with anti-cheat, or on RX 9000 GPUs. No performance gain is guaranteed on
your Deck; compare the same scene and settings.

Select Exact or 4.1.1b to switch back, or **Restore bundled upscaler** in Setup.
The archive and the specific DLL in its `exact/` or `lossy/` directory are both
verified by SHA-256 before installation. Setup identifies the installed build by
its bytes. OptiScaler reports `4.1.1-igpu-cyboman` for Exact and
`4.1.1-igpu-lossy-cyboman` for Lossy. Frame generation is configured separately.

## Original 4.1.1b preset

Close the game, install OptiScaler through the plugin if needed, and select
**FSR 4.1.1b — Steam Deck** under Basic → Override upscaler with. The first use
requires a download (about 3.5 MB); later games reuse the verified cached DLL.
Download or validation failure leaves the previous DLL and settings intact.

This option installs the community `amd_fidelityfx_upscaler_dx12.dll` from
[the3rdparty1917/fsr4xyz 4.1.1b](https://github.com/the3rdparty1917/fsr4xyz/releases/tag/4.1.1b).
The release describes an RDNA2 ghosting fix. Archive and DLL SHA-256 values are
pinned in the plugin. The SDK's version resource still says 4.1.1, so Setup
identifies the build by its bytes instead of relying on that version string.

The plugin still bundles OptiScaler runtime **0.9.4**, including the original
SDK **4.1.1**. OptiScaler Client **1.0.7** is a separate management application;
it is not required or installed by this plugin.

## Settings and verification

The option selects the FidelityFX backend (`fsr31` for DX12), sets
`Fsr4ForceEnableInt8=true`, `UpscalerIndex=0`, and resets `Fsr4Update` and
`Fsr4Preset` to `auto`. DX11/Vulkan select the existing DX12 bridge backend.
INT8 initialization requires a fresh game launch. Per-game compatibility still
applies; the preset cannot add upscaler inputs to an unsupported game.

Launch the game and use its supported upscaler input (for example XeSS in the
Cyberpunk setup tested here). Enable the FSR watermark in OptiScaler to confirm
`FSR4-I8`; plain FSR3 indicates fallback. Setup identifies the installed patch,
while the watermark identifies the model actually running.

This is experimental community support for RDNA2. Evaluate motion/ghosting,
image quality and base frame rate in the same scene before and after enabling.
It does not fix or enable FSR4 frame generation. You may keep FSR3 frame generation
with FSR4 upscaling; test stability separately. Avoid modified DLLs in games whose
anti-cheat forbids them.

## Switching back

Choose FSR 3.X or another upscaler in Basic settings to change the active backend.
The community DLL stays installed for later use. To remove the patch, close the
game and choose **Restore bundled upscaler** in Setup. This keeps settings intact;
INT8 configured by hand or retained after restore is labelled **FSR 4 INT8 (manual)**.

Reinstall preserves a verified community DLL. If that DLL is missing or altered,
reinstall stops with repair instructions instead of silently replacing the patch.
Select the Steam Deck option again to repair it, or restore the bundled DLL.
Uninstall restores the game's original backed-up files, not the OptiScaler SDK.

The source release and pinned hashes should be reviewed before updating to a new
community build. Older 4.0.2 community variants are outside this feature's scope.
