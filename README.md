# OpenMW-PostProcessShaders
Some post process shaders for OpenMW 0.48+
https://www.nexusmods.com/morrowind/mods/53747

# Shaders
**BloomPS2**: 
Bloom shader similar to the PS2 era (Ico, Shadow of the Colossus) or Oblivion. Purposely low res RT so its shimmery and has a glow around the outer edge of the frame. Has settings to change brightness and threshold, and a skybox mask to lower sky brightness, can also be tinted to different colours. May have some issues with the built in fog when adjusting the sky brightness. Based on: https://github.com/Matsilagi/RSJankShaders/blob/main/Shaders/BadBloomPS2.fx

RT resolution is set to 1/8th res to match the PS2, but this causes heavy shimmer in motion, this can be changed by editing the 'width_ratio' and 'height_ratio' of the render targets.

**BloomKawase**:
Modified version of BloomPS2 which uses a Kawase blur instead, also added more customization settings and dither debanding. 

**Lens-Flare**:
Port of https://john-chapman-graphics.blogspot.com/2013/02/pseudo-lens-flare.html, Kind of sucks during the day because of the lack of true HDR rendering, but looks decent at night or inside. Also has a 'Disable Sky' variable that allows you to use it in conjunction with Sun-Flare as the sun instead of trying to wrangle image brightness.

**Sun-Flare**:
Modified version of Lens-Flare that only applies to the sun. Use in combination with Lens-Flare's 'Disable Sky' variable to get a sun flare while keeping interior flares or separate flare settings

**ClampColours**:
Clamps colour depth to assigned value, was using for debugging, probably not useful.

**Dither4x4 / Dither8x8**:
Ordered Bayer dithering using either a 4x4 or 8x8 matrix texture. Clamps colours and then uses the ordered dithering to reconstruct depth. Not really useful, just a novelty.

**QuakeUnderwater**: 
Underwater screen distortion similar to Quake's software renderer. Default settings might be a bit intense but with proper settings it can look quite nice. A port of this Shadertoy: https://www.shadertoy.com/view/MsKXzD

**ValveDither**: 
Valve's screen space dithering, should theoretically improve colour banding but I could never get it to really work. Has ClampColours built in so you can limit colour depth and have it reconstructed with dither, better results than Dither4x4/8x8, but still just a novelty.

**Saturate**: 
Modified the sample shader to just invert the desaturation value, so it saturates colour instead.

**Pixelate**: 
Pixelate the screen by rendering to a lower res render target with min/mag set to nearest. Can't expose strength settings since its a render target, but you can change the RT size inside the source if you want more or less pixelation.

**SMAA**:
SMAA Anti Aliasing, port was NOT done by me, it was done by someone else who deleted their shaders without warning, just re-uploading so that people can use it.

**XERO-LUT**:
A basic LUT shader, ported from MGEXE. Uses the LUT texture 'XERO-lut.tga', so if you want to use your own LUT replace this texture. The default LUT is in the DirectX UV format, but OpenMW is OpenGL, so the Y axis is flipped automatically by the shader for using DirectX format textures. I added a uniform to toggle this flipping, so if your LUT looks like a clown vomitted, try switching the flip.

**Gaussian/KawaseBlur**:
Standalone Gaussian/Kawase blurs. Can set the strength to negative to get a sharpen filter. Gaussian is much more expensive than Kawase but produces a nicer looking blur.

**WaterFog**:
Volumetric underwater fog. Based on this paper: https://www.terathon.com/lengyel/Lengyel-UnifiedFog.pdf

**Caius**:
Live Caius Cosades reaction.

**Caustics**:
Sort of hacky underwater caustics. They will only appear above water if you have 'Refraction' disabled in the water settings, but they still blend incorrectly and look bad at a distance.
