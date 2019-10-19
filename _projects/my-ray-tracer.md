---
layout: post
title:  "My Very Simple Ray Tracer Implementation"
date:   2015-10-13 20:45:00 -0500
categories: [jekyll]
---

Recently I was going over my over project files and I came across the Ray Tracer project I did for my university graphics course. It's a very simple ray tracer implementation written in C++ and Lua. Here you can read about all the features and objectives I was trying to achieve.

## Introduction
This is the final project for CS488: Introduction to Computer Graphics in University of Waterloo. In this project, a ray tracer has been constructed using C++ and Lua. This ray tracer has several features that will be introduced as objectives.

The scene to be rendered involves a bumped stone wall as a background, a texture mapped desk as the surface, and some objects on the desk. The objects includes transparent spheres, solid metal sphere that reflect lights, and some other primitives and 3D models.

## Purpose
1. Accelerate the speed to render a scene using ray tracer.
2. Render scenes that contains reflection and refraction effects.
3. Create other primitives so that the ray will be calculated faster.

## Technical outline
Uniform spatial subdivision will divide the space into smaller cubes. Only the objects within the a cube will be tested with the ray if the ray passes the cube. This feature accelerates the rendering speed because it avoids brute-force search approach.

Reflection requires secondary rays to cast from point of contact from primary ray to the surface reflection direction and render the color of the second point of contact. if the ray contacts a reflective surface again, another ray will be casted.

Refraction feature is achieved by casting secondary ray into the object with a certain angle and returns the color behind the object.

Mapping textures to surfaces using coordinates conversion from 3D to 2D.

Define New primitives, such as cone, cylinder.

Display caustics. Secondary rays will be casted from the point of contact by the primary ray to each light source. If the ray passes a transparent sphere, light will be bent.

To achieve soft shadows effect, light source will be a sphere instead of a single point. Cast multiple rays from the light source to the point to achieve soft shadows.

Bump-mapping applies a different normal to the 3D surface from a 2D surface bump map.

### Reflection

![reflection](/assets/images/ray-tracer/reflection.png)

#### Technique
Reflection is achieved by using recursive rays. When the primary ray (which is the ray sent from the eye to the the scene through each pixel on the screen) hits a reflective object, a secondary ray will be sent out from the point of contact to the reflection direction. When the secondary ray hits another object, it will return the color of the hit object. The final color is calculated by adding the color of the object and the color of the reflection:

```
Final_color = Object_color + reflected_color.
```

### Refraction

![reflection](/assets/images/ray-tracer/refraction.png)

#### Technique

Refraction is also achieved by using recursive rays. When the primary ray hits a refractive object, a secondary ray will be sent out from the point of contact into the object with the calculated refraction angle. Then the secondary ray will travel within the object and hit the boundary of the object again. This time the refraction angle is calculated again from the inner object to the outer space and a third ray will be sent out. The third ray determines the color of the refractive ray. The final color is calculated by adding the color of the object and the color returned by the refractive ray.

```
Final_color = Object_color + refracted_color.
```

### Texture mapping

#### Wall texture:
![Brick wall texture](/assets/images/ray-tracer/brick_wall_texture.png)

#### Desk texture:
![Desk texture](/assets/images/ray-tracer/wood_texture.png)

#### Texture mapped result
![Texture mapping](/assets/images/ray-tracer/texture_mapping.png)

### Additional primitives: Cone and Cylinder
![Cone and Cylinderder](/assets/images/ray-tracer/cone_cylinder.png)

### Soft shadows
#### Without soft shadow:
![Sharp shadow](/assets/images/ray-tracer/sharp_shadow.png)

#### With soft shadow:
![Soft shadow](/assets/images/ray-tracer/soft_shadow_1.png)

### Multi-processing using threads
![threads](/assets/images/ray-tracer/threads.png)

### Bump mapping

#### Scene without bump mapping:
![No bump mapping](/assets/images/ray-tracer/bump_mapping_1.png)

#### Scene with bump mapping and light on the right:
![bump mapping right](/assets/images/ray-tracer/bump_mapping_2.png)

#### Scene with bump mapping and light on the left:
![bump mapping left](/assets/images/ray-tracer/bump_mapping_3.png)

### Final scene
![Final scene](/assets/images/ray-tracer/final.png)