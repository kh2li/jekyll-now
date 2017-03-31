### Objective 1 - Grid based acceleration
![Grid Acceleration]({{ site.url }}/images/Objective1Scene.png)

At 500x500 px resolution (above is 1000x1000)

| Grid Dimensions     | CPU time (s) |
|-------------------  |--------------|
| 15x15x15            | 1845         |
| 22x22x22            | 942          |  
| 26x26x26            | 721          |  
| 30x30x30            | 577          |

### Objective 2 - Texture mapping
![Texture Mapping]({{ site.url }}/images/Objective2.png)

### Objective 3 - Bump mapping
![Texture Mapping]({{ site.url }}/images/Objective3.png)

### Objective 4 - Refraction
![Refraction]({{ site.url }}/images/Objective4.png)

### Objective 5 - Depth of field
![Depth of Field]({{ site.url }}/images/Objective5.png)
![Depth of Field]({{ site.url }}/images/Objective5b.png)

### Objective 6 - Glossy reflection
![Glossy Reflection]({{ site.url }}/images/Objective6.png)

### Objective 7 - Glossy transmission
![Glossy Transmission]({{ site.url }}/images/Objective7.png)

### Objective 8 - Soft shadows
![Soft Shadows]({{ site.url }}/images/Objective8.png)

### Objective 9 - Antialiasing
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
