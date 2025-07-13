# Nebula (coming soon)

![Contrast Render Banner](../../assets/pro_atmo/nebula/nebula.jpg)

## About

This addon allows you to create volumetric nebulae in Blender. The created nebula object contains a custom shader, which enables super fast render times.

Since the shader uses light samples within the shader itself, it will not iteract with seperate lightsources our other objects in the scene.

Furthermore, the nebula density adjusts automatically to the object scale, so that the appearance does not change. When scaling down, the overall density goes up, so that the realtic volume "particles" stay the same.

## Getting Started

After enabling the addon, you can add nebulaes to the scene by using the "Add" button on the "Nebula" panel which you can find at: 3d viewport -> n-tab -> Pro Atmo -> Nebula.

When a nebula object is selected, you can change its appearence by tweaking the displayed properties.

## Properties

### Color

The color of the nebula can be adjusted by using the following properties:

**Scattering Color:** When perfect white light is shining onto the particle, this color gets emitted.

**Scattering Intensity:** Scales the scattering color by this value.

**Absorbtion Color:** When perfect white light is shining onto the particle, this color gets absorbed.

**Absorbtion Intensity:** Scales the absorbtion color by this value.

### Density

The overall shape of the nebula is defined by the density. The nebula uses a noise texture which is offset by another noise texture, so that the shape gets a bit interrupted. You can try out different parameters in order to get the result you want.

if you want to change the overall density of the nebula, you can do so by using the **density**, **densiy bias** or **density map range** properties.

**density**: overall density.

**density bias**: The density texture outputs values ranging from 0 to 1, the density bias is used as an exponent for that function.

**density map range**: defining an upper and lower bound for the density, which is used for the density texture.

When tweaking these parameters, you can toggle the shader output to the density by using the **Toggle Density** button, so that changes can be seen clearly.

### Light

The nebula uses a light source which is set to the center by default. This light is not like a point light, but rather that a sphere full of light, which is weaker at greater distances to the center. The center of this light can be offset by using the **Light Position** property. The color and intensity can also be changed by using the **Color** and **intensity** properties.

## Render Settings

### Volume Step Rate

When Rendering volumetric objects, the render engine needs to convert the 3d data into 2d data, which is then displayed onto the 2d screen.

The volume step rate describes how many steps or sample points are used for that process. When an object has a lot of details in it, more steps are required for a good 2d approximation of that object.

Using smaller steps results into more sample points which can be used, which gives a higher quality.

By default the step rate is set to 1 which does not give optimal results. Depending on your system (gpu) you might want to set this value to 0.1 for the viewport and 0.01 for rendering.

### Max Volume Steps

If your using a low volume step rate, the number of steps can be very high for thicker parts of the object. You can limit the amount of steps by using the max volume step rate, so that you are not using unnessary steps.

Because the nebula object has roughely the same thickness in every direction, you can ignore this value for the most part, but you can keep it at around 1000, to make sure you are never using more than 1000 steps which should be more than enough.

### Light Absorbtion Iterations

When a particle is rendered, it not only needs to know which density and color it has, but also how much light from the light source is reaching it. For that reasen, the shader calculates how much light is absorbed by the particles between the light source and itself. Using more iterations or steps for that process results into a better light approximation.

for the final render you should use the maximum amount of light absorbtion iterations.

### Render Samples

because the shader itself already does a lot of light calculations, you dont need much samples in order to get a high quality render. I would recommend using between 4 and 16 samples per frame.
