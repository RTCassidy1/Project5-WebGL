-------------------------------------------------------------------------------
CIS565: Project 5: WebGL
-------------------------------------------------------------------------------
![Globe](https://raw.githubusercontent.com/RTCassidy1/Project5-WebGL/master/Renders/globeWithBumpAndWater.bmp)

-------------------------------------------------------------------------------
Wave
-------------------------------------------------------------------------------
* For the Wave I tried out several different vertex shaders, but the one that looked the coolest to me was just changing the + to a * in the sin and cosine function.  This basically made the frequency of the wave oscilate in both directions which made some really neat looking visuals
![Wave](https://raw.githubusercontent.com/RTCassidy1/Project5-WebGL/master/Renders/Wave.bmp)
-------------------------------------------------------------------------------
Globe
-------------------------------------------------------------------------------
* For the globe I did several things.  For night I diffuse shaded the texture as if the light was opposite the sun which made the transition from day to night look a lot nicer in my opinion.
* I set the gamma to 1.0, but I multiplied the nighttime diffuse component by 3 to get a nice look.
* I implemented the bump mapping for the land.
* I also implemented procedural bump mapping for the water.  I did this using a perlin noise generator I got from https://github.com/ashima/webgl-noise  I then sampled the noise in center, top and right pixels as if it were a height map and used this to transform the normals.  I also added some coefficients to adjust the size of the texture and the depth of the height map.
* I added a time component and used it to shift the cloud position as well as to animate my perlin noise so the water shimmered.

-------------------------------------------------------------------------------
PERFORMANCE EVALUATION
-------------------------------------------------------------------------------
I'm running on a 2.7ghz i7 macbookPro with a NVIDIA GeForce GT 650M 1024 MB video card.  All my tests were done in firefox.

There are several components I added to the shader that should have slowed it down a bit, however it still runs fine in real time so nothing was TOO intense.
* I have an if statement to decide whether I'm shading day or night.  I could probably go back and find a way to do that without an if statement that would speed things up a little.
* adding the bump mapping, and the cloud texture map added additional memory lookups.  It only required one extra lookup per pixel for the clouds, but 3 for the bump since I have to look at 3 different positions.
* looking up the specular map for the water is also an additional lookup, but I get to use this same value to tell me if i'm in water or not for the water bump map.
* I also have an if statement to decide if I'm in the water or not. and whether to texterue. This too could probably be avoided.
* If I keep the if statement, I could move the perlin noise generation inside it for some speed increases.  Currently I do the noise lookup on every fragment, regardless of whether or not it is actually water.
* The Procedural perlin noise generation adds a lot of computation as I have to compute the noise 3 times for each fragment.  It would be interesting to see if it is faster to generate it procedurally each time, or to generate it once, save it to memory, and do memory lookups every time.


-------------------------------------------------------------------------------
THIRD PARTY CODE POLICY
-------------------------------------------------------------------------------
* To create the perlin texture I used code from https://github.com/ashima/webgl-noise
-------------------------------------------------------------------------------
Video Links
-------------------------------------------------------------------------------
http://youtu.be/pANBT5FVIA4
http://youtu.be/Eq3gdeBmovE
