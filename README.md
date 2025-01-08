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
Port of https://john-chapman-graphics.blogspot.com/2013/02/pseudo-lens-flare.html, Kind of sucks during the day because of the lack of true HDR rendering, but looks decent at night or inside. Also has a 'Disable Sky' variable that allows you to use it in conjunction with Sun-Flare as the sun instead of trying to wrangle image brightness. It is very expensive because it uses a gaussian blur, even more expensive if you combine it with Sun-Flare or the built in BloomLinear shader.

**Sun-Flare**:
Modified version of Lens-Flare that only applies to the sun. Use in combination with Lens-Flare's 'Disable Sky' variable to get a sun flare while keeping interior flares or separate flare settings. It is very expensive because it uses a gaussian blur, even more expensive if you combine it with Lens-Flare or the built in BloomLinear shader.

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
Pixelate the screen.

**SMAA**:
SMAA Anti Aliasing, port was NOT done by me, it was done by someone else who deleted their shaders without warning, just re-uploading so that people can use it. Edited to use 0.49+ dropdown selections, so requires 0.49+. An alternative probably more optimized version is available from the original port author here: https://www.nexusmods.com/morrowind/mods/53667

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

**ColorMood**:
Ported from MGEXE, basic colour adjustment.

**Neon**:
Just a fun little thing, adds rainbow neon outlines around everything using the scene normal derivatives, because of that its a bit crusty looking. Pairs well with the Neon Vivec mod and some cranked up bloom.

**JPEG**:
It's what it says on the tin, JPEG compression with an adjustable strength. Port of https://www.shadertoy.com/view/llfyz4 but I might improve it later.

**Distortion Debug**:
I needed something to help me while working on a mod using the 0.49 distortion feature. This shader only works in 0.49+ and uses the new choice box dropdown widget, how fancy.

**Underwater Tweaks**:
A combination of KawaseBlur, Saturate, and the built in adjustments shader, set to only be enabled underwater. Place near the bottom of your shader stack, meant to pair with Caustics and WaterFog (which should both go near the very top, caustics above waterFog. Also pairs well with QuakeUnderwater with more toned down settings.

**Retro Dither**:
PSX style dithering shader, ported from https://www.shadertoy.com/view/tlc3DM, which was ported from https://github.com/jmickle66666666/PSX-Dither-Shader/

**Point Glow**:
A standalone version of the Point Glow effect from Zesterer's Clouds shader. All credits go to Zesterer, I just ripped it out and made it standalone. https://github.com/zesterer/openmw-volumetric-clouds

**Rain Drops**:
Applies raindrops to the 'camera lens' when its raining.
