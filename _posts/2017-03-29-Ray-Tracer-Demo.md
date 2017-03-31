### Objective 1 - Grid based acceleration
To reduce the number of intersections each ray has to test, we can use a 3D grid to partition the primitives in the scene and only test for intersections against primitives in the cells the ray encounters. The method described in the paper A Fast Voxel Traversal Algorithm for Ray Tracing by Amanatides and Woo was implemented to traverse the grid. First we determine where the ray starts in the grid by either looking at the origin of the ray or the intersection point of the ray and the bonding box of the grid. Next we set the step direction of the ray and calculate how far the ray must travel to reach a new grid going only in that direction. The shortest of X, Y, Z will determine which cell the ray will go into after leaving the current cell. When the ray enters a new cell, a new t is calculated for the direction it entered.

![Grid Acceleration]({{ site.url }}/images/Objective1Scene.png)

At 500x500 px resolution (above is 1000x1000)

| Grid Dimensions     | CPU time (s) |
|-------------------  |--------------|
| 15x15x15            | 1845         |
| 22x22x22            | 942          |  
| 26x26x26            | 721          |  
| 30x30x30            | 577          |

### Objective 2 - Texture mapping
Given an image and the UV coordinates, we can map a color from the image on to a point on the primitive. For spheres we look at the intersection point and determine the UV by looking at the angels of the intersection. For a cube, we determine which face the intersection point is on and what are the local coordinates with respect to that face based on a corner and its two edges as a basis. For meshes we can take any two edges of a triangle and use the cross product to produce a normal vector. If the vertex normals are provided we can use Barycentric coordinates to interpolate the normal of a point in the triangle.

![Texture Mapping]({{ site.url }}/images/Objective2.png)

### Objective 3 - Normal mapping
Using the same method as texture mapping we can map the normals like we map the color. We interpret the color (R,G,B) as (X,Y,Z)[-1,1] direction of the normal. (128, 128, 255) is considered no perturbation (which is (0,0,1)), so for any normal vector returned by the normal map, we determine the rotation matrix need to rotate the (0,0,1) vector to the given vector and apply this rotation matrix on the face normal of the triangle.

![Texture Mapping]({{ site.url }}/images/Objective3.png)

### Objective 4 - Refraction
Refractions are achieved by allowing rays to go through a primitive rather than bounce based on Schlick's approximation of the Fresnel equation for determining what is the percentage of light gets reflected and what percentage of light gets refracted. Based on the material's Index of Refraction and the entering medium's IOR, we can determine the angle at which ray will move when it refracts.

![Refraction]({{ site.url }}/images/Objective4.png)

### Objective 5 - Depth of field
Depth of field is achieved by shooting multiple rays from the camera at different points in a direction towards a point on a plane that is a certain distance away based on where we want to focus. If the object intersection point is on the focus point then all the camera rays will land on the same spot and the returned pixel color will all be the same. The further away from the plane the intersection occurs at the blurrier it will appear as the rays intersect at points further away from one another.

![Depth of Field]({{ site.url }}/images/Objective5.png)
![Depth of Field]({{ site.url }}/images/Objective5b.png)

### Objective 6 - Glossy reflection
Glossy reflection is achieved by shooting multiple rays out during reflection and averaging the result. The rays have the direction perturbed based on the Phong exponent. The larger the number, the sharper the reflection as the ray deviates from a perfect specular reflection. The distribution of the directions follow a cosine distribution.

![Glossy Reflection]({{ site.url }}/images/Objective6.png)

### Objective 7 - Glossy transmission
By combining the work of glossy reflection to perturb reflected rays and refraction to transmit rays, we get glossy transmission.

![Glossy Transmission]({{ site.url }}/images/Objective7.png)

### Objective 8 - Soft shadows
Instead of having a point light, area lights are defined and instead of a single shadow ray to each point light, multiple shadow rays are sent to randomly picked points on the area light. The more shadow rays that reach the light, the brighter the spot will be. The shadow will gradually decrease in strength as the points can gradually hit more light points as it gets away from the shadow casting object.
![Soft Shadows]({{ site.url }}/images/Objective8.png)

### Objective 9 - Antialiasing
A 2x2 grid is used to calculate the colors first and if the colors are not all within a certain threshold of one another then a NxN jitter grid is used. The average color of each ray is taken to determine the color of the pixel.

![Antialiasing]({{ site.url }}/images/Objective9.png)

### Objective 10 - Final Scene

![Final Scene]({{ site.url }}/images/Objective10b.png)

### Extra - Phong Shading
![Final Scene]({{ site.url }}/images/ObjectiveExtraPhongShading.png)

### Extra - Photon Mapping
![Final Scene]({{ site.url }}/images/ObjectiveExtraPhotonMapping1.png)
![Final Scene]({{ site.url }}/images/ObjectiveExtraPhotonMapping2.png)
![Final Scene]({{ site.url }}/images/ObjectiveExtraPhotonMappingC.png)

### Extra - Multithreading
Rendering the Image in Objective 1 at 300x300 px

| # Threads     | CPU time (s)  | Real time (s)  |
|-------------  |-------------- |----------------|
| 1             | 279           | 280            |
| 2             | 280           | 145            |  
| 3             | 284           | 97             |
| 4             | 283           | 96             |
| 5             | 284           | 95             |
| 6             | 285           | 96             |
| 7             | 285           | 96             |   
| 8             | 284           | 96             |
