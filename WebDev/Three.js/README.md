[ZTM Three.js](https://www.youtube.com/watch?v=KM64t3pA4fs)
[Robot Bobby - YouTube](https://www.youtube.com/@robotbobby9)

<details>
  <summary>Basics</summary>

# Basics:

```javascript
 import * as THREE from 'three';

  componentDidMount() {
 
    // LOAD SECENE
    
    const canvas = document.getElementsByClassName("webgl")[0];
    const scene = new THREE.Scene();
    
    // --OBJECT
    
    const geometry = new THREE.BoxGeometry(1, 1, 1);
    const material = new THREE.MeshBasicMaterial({ color: "red" })
    const cube = new THREE.Mesh(geometry, material);
    scene.add(cube);
   
    // --CAMERA
      const sizes = {
       width: 800,
       height: 600
       }

    // THREE.PerspectiveCamera( fieldview [in degree] ,aspect value [= width of render / height of render]);
   
    const camera = new THREE.PerspectiveCamera(75, (sizes.width / sizes.height));
    camera.position.z = 3;
    camera.position.y = 1;
    camera.position.x = 1;
    scene.add(camera);
    
    
    // --RENDERER
    
    // console.log(canvas);
    const renderer = new THREE.WebGLRenderer({
      canvas: canvas
    })
    renderer.setSize(sizes.width, sizes.height);
    renderer.render(scene, camera);
  }

  render() {
    return(

      <div>
        <canvas className="webgl"></canvas>
      </div>
    )
  }
export default App
```





<details>
  <summary>TRANSFORM</summary>

## TRANSFORM:
- position
- scale
- rotation
- quaternion

>NOTE : rotation and quaternion both are used for rotation and if any of them is changed then both changes.

>POSITION : 
- y ==>up , down
- z ==> backward , forward
- x ==> right , left

position is a vector in 3D
```javascript
   // This outputs the length of vector from origin to object
   console.log( mesh.position.length() );
   
   // This outputs distance between 0,1,2 vector and mesh
   console.log( mesh.position.distanceTo(new THREE.Vector3(0,1,2)) );

   // This outputs distance between mesh and camera
   console.log( mesh.position.distanceTo(camera.postion));

   // directly make all positions = 1
   mesh.position.normalize();


   camera.position.x = 1;
   camera.position.y = 2;
   camera.position.z = 3;
   // position can be set by ::
   camera.position.set(1,2,3);

```


> AXES HELPER :
```javascript
    // --AXES HELPER
    // THREE.AxesHelper( length of all axis );

    const axeshelper = new THREE.AxesHelper(2);
    scene.add(axeshelper);
```


> SCALE :
```javascript
	// mesh.scale.x = length ;
	mesh.scale.x = 2 ;
	// This extends the object in x by 2 so that it is of 2 units 

	// we can also use set to set all
	mesh.scale.set(2,1,1); // same as mesh.scale.x = 2;
```

> ROTATION :
```javascript
	// rotation of x,y,z is Euler
	// angles are measured in PI = 3.1459
	mesh.rotation.x = (Math.PI/4);
```

> NOTE : When one axis is rotated then all axis are affected therefore, sometimes it might happen where you can't rotate your axis anymore, THIS IS CALLED GIMBAL LOCK
>   >to solve this we can use :
```javascript
	object.rotation.reorder("yxz");
```
> Euler is therefore problematic therefore we use QUATERNION

> QUATERNION : [Visualizing quaternions (4d numbers) with stereographic projection - YouTube](https://www.youtube.com/watch?v=d4EgbgTm0Bg)

</details>

<details>
  <summary>LOOK AT THIS</summary>

## LOOK AT THIS ! 
```javascript
	// lookAt() is used to look at something
	camera.lookAt( new THREE.Vector3(0,0,0) );
	camera.lookAt( mesh.position );
```

</details>


<details>
  <summary>ANIMATIONS</summary>


## ANIMATIONS :
```javascript
	// requestAnimationFrame function calls tick function at a rate of frame of second according to computer.
	// like 60 frame/sec will cal this function 60 times in one sec.
	const animate =()=>{
      cubegroup.rotation.y += 0.01;
      renderer.render(scene, camera);
      window.requestAnimationFrame(animate);
    }
    animate();
    
    //This method depends on each computer frame per second

	// TO overcome above this issue we use ::
	let time = Date.now();
	
    const animate =()=>{
      const currentTime = Date.now();
      const deltaTime = currentTime - time;
      time = currentTime;
  
      cubegroup.rotation.y += 0.001*deltaTime;
      renderer.render(scene, camera);
      window.requestAnimationFrame(animate);
    }
    animate();



	//OR we can use CLOCK OF THREE.js


    const clock = new THREE.Clock();
    
    const animate =()=>{
        const elapsedTime = clock.getElapsedTime();
        cubegroup.rotation.y = elapsedTime * (Math.PI*2);
        
        // To make 1 revolution per second

        renderer.render(scene, camera);
        window.requestAnimationFrame(animate);
      }
      aniimate();


```

</details>


<details>
  <summary>CAMERA</summary>

## CAMERA :
- Array Camera : to make an array of cameras on same scene like how two players on same scene see differently.
- Stereo Camera : for VR effects , its like seeing from both eyes.
- Cube Camera : six cameras are placed like six faces of cube around the scene. 
- Orthographic Camera : camera without perspective (size of object remain same irrespective of how far camera is) .
- Perspective Camera : size of objects changes according to camera.

```javascript
// ====================================================================
// ===                        Perspective Camera                    ===
// ====================================================================

// THREE.PerspectiveCamera( fieldview [in degree] ,aspect value [= width of render / height of render] , near , far );
// here near and far are max and min values of view range. Anything going outside that is not rendered

// try changing far to 2 or 3 to check limits here.
const camera = new THREE.PerspectiveCamera(75,(size.width / size.height), 1, 100);
    camera.position.z = 2;
    camera.position.y = 1;
    camera.position.x = 2;
    scene.add(camera);
    camera.lookAt(mesh.position);

// ====================================================================
// ===                       Orthographic Camera                    ===
// ====================================================================
// const camera = new THREE.OrthographicCamera( left, right, top, bottom, near, far );
// orthographic camera renders a cuboid having parallel axes on left , right, top, bottom
// BUT as it forms cuboid acc. to the size of renderer frame so when we form a cuboid it is with respect to size so to fix this we can multiply left and top with aspect ratios adjust the size of mesh(cube formed).

```


## Custom Controls for Camera :
> Custom Controls for Camera using mouse :
```javascript
const cursor ={
  x:0,
  y:0
}

// below we converted mouse position into a range of (-0.5, 0.5) value
canvas.addEventListener('mousemove', (event)=>{
  cursor.x = -(event.clientX/size.width - 0.5);
  cursor.y = event.clientY/size.height - 0.5;
})

const camera = new THREE.PerspectiveCamera(75,(size.width / size.height), 1, 100);
// we wont assign x and y position of camera as they depends on mouse now.
// assign z other wise it wont have any reference
camera.position.z = 4;
scene.add(camera);

// we only want to circulary move camera on 'x' and 'z' axis
const animate =()=>{
  camera.position.x = Math.sin(cursor.x*Math.PI*2)*4;
  camera.position.z = Math.cos(cursor.x*Math.PI*2)*4;
  camera.position.y = cursor.y*6;
  camera.lookAt(mesh.position);
  
  renderer.render(scene,camera);
  window.requestAnimationFrame(animate);
}
animate();
```


> Built-in Controls for Camera :
```javascript
// ====================================================================
// ===                        Orbit Controls                        ===
// ====================================================================

// We have to explicity import Orbit Controls from examples as they are not available in THREE object.

// Orbit controls ==> 
// Left mouse drag to change 'camera' position
// Right mouse drag to change 'axis' or '(0,0,0) coordinates' postion
// Scroll to zoom in and out.

import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls.js'

const camera = new THREE.PerspectiveCamera(75,(size.width / size.height), 1, 100);
// camera inital position
camera.position.z = 4;
camera.position.y = 1;
camera.position.x = 2;
scene.add(camera);
// you can remove lookAt on camera here as we would be using Orbit Controls and in Orbit Controls lookAt wont work
// camera.lookAt(mesh.position);

// --Controls
const controls = new OrbitControls(camera, canvas);
// [IMP] We can set reference point or 'axis' or '(0,0,0) coordinates' postion of camera by controls.target
// if we set target to mesh.position it somewhat same as lookAt, just play around them to adjust your need
// [Note] By setting target as mesh.positon we basically fixed the mesh and therefore right mouse drag wont change the mesh BUT would change the axis.
// comment below target
controls.target = mesh.position;

// Damping gives a smooth transition of camera postion making it more realistic.
controls.enableDamping = true;


const animate =()=>{

  // [IMP] its important to update the controls on every frame
  controls.update();

  renderer.render(scene,camera);
  window.requestAnimationFrame(animate);
}
animate();
``` 

</details>


<details>
  <summary>Full-Screen and Resizing of Canvas</summary>

## Full-Screen and Resizing of Canvas :
```css
#root, body, html {
  margin: 0;
  padding: 0;
  overflow: hidden;
}

#webgl{
  position: fixed;
  left: 0;
  top: 0;
  outline: none;
}
```
---
```javascript
// ====================================================================
// ===                        Full Screen                           ===
// ====================================================================

window.addEventListener('dblclick', ()=>{
  const fullScreenElement = document.fullscreenElement || document.webkitFullscreenElement;
      
  if(!fullScreenElement){
	if(canvas.requestFullscreen) canvas.requestFullscreen();
	else if(canvas.webkitRequestFullscreen) canvas.webkitRequestFullscreen();
  } else {
	if(document.exitFullscreen) document.exitFullscreen();
	else if(document.webkitExitFullscreen) document.webkitExitFullscreen();
  }

})



// ====================================================================
// ===                      Resizing Screen                         ===
// ====================================================================

const size = {
  width: window.innerWidth,
  height: window.innerHeight
}

window.addEventListener('resize',()=>{

  // Update sizes
  size.width = window.innerWidth;
  size.height = window.innerHeight;

  // Update camera
  camera.aspect = size.width/size.height;
  camera.updateProjectionMatrix();

  // Update Renderer
  renderer.setSize(size.width, size.height);


  // Adjust the pixel ratio to avoid blurry output on high DPI screens
  renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
})
```

</details>


<details>
  <summary>GEOMETRY</summary>

## GEOMETRY :
- Geometry is composed of vertices (point coordinates in 3D space) and faces (triangles that join those vertices to create a surface)
- can be used for meshes but also for particles (in particles each vertex acts as particle)
- can store more data than the positions (UV coordinates, position, normals, colors, size or anything we want)

> Built-in Geometry (inherit from BufferGeometry class) :
- Box 
- Plane 
- Circle 
- Cone 
- Cylinder
- Ring
- Torus (donut)
- Torus Knot 
- Dodecahedron
- Octahedron
- Tetrahedron
- Icosahedron
- Sphere
- Shape (based on curves)
- Tube
- Extrude
- Lathe
- Text

- Box Geometry : 
	width — Width; that is, the length of the edges parallel to the X axis. Optional; defaults to `1`.  
	height — Height; that is, the length of the edges parallel to the Y axis. Optional; defaults to `1`.  
	depth — Depth; that is, the length of the edges parallel to the Z axis. Optional; defaults to `1`.  
	widthSegments — Number of segmented rectangular faces along the width of the sides. Optional; defaults to `1`.  
	heightSegments — Number of segmented rectangular faces along the height of the sides. Optional; defaults to `1`.  
	depthSegments — Number of segmented rectangular faces along the depth of the sides. Optional; defaults to `1`.

> Wireframe: shows a wired frame of mesh
```javascript
const mesh = new THREE.Mesh(
  new THREE.BoxGeometry(1,1,1),
  new THREE.MeshBasicMaterial({color : 'red', wireframe: true})
);
``` 

> Built-in Geometries : 
```javascript
const geometry = new THREE.SphereGeometry(1,32,32);
const geometry = new THREE.ConeGeometry(1,1,32);
const geometry = new THREE.TorusGeometry(1,0.4,32,100);
const geometry = new THREE.TorusKnotGeometry(1,0.4,32,100);
``` 

> Create Custom BufferGeometry :
```javascript
const geometry = new THREE.BufferGeometry()
const positionArray = new Float32Array([
	0,0,0, // First Vertex
	0,1,0, // Second Vertex
	1,0,0  // Third Vertex
]);
const positionAttribute = new THREE.BufferAttribute(positionArray, 3);
// 'position' below is a Three.js default shader
geometry.setAttribute('position', positionAttribute);

const mesh = new THREE.Mesh(
  geometry,
  new THREE.MeshBasicMaterial({color : 'red', wireframe: true})
);
scene.add(mesh);
```
---
```javascript
const geometry = new THREE.BufferGeometry()
const count = 50; // Number of faces

const positionArray = new Float32Array(count*3*3); // each face have 3 vertices and each vertex have 3 coordinates (x,y,z)

for(let i=0; i<count*3*3; i++){
  positionArray[i] = Math.random() * 4;
}

const positionAttribute = new THREE.BufferAttribute(positionArray, 3);
geometry.setAttribute('position', positionAttribute);

const mesh = new THREE.Mesh(
  geometry,
  new THREE.MeshBasicMaterial({color : 'red', wireframe: true})
);
scene.add(mesh);
```
</details>


<details>
  <summary>Debug UI for JavaScript (lil-gui)</summary>

## Debug UI for JavaScript (lil-gui) :
```javascript
import gsap from "gsap";
import GUI from 'lil-gui';

//==================Debug===================
const gui = new GUI();
window.addEventListener('keydown', (event)=>{
  if(event.key === 'h'){
	if(gui._hidden) gui.show();
	else gui.hide();
  }
});
const parameters = {
  faces:50,   // Number of faces
  spin: ()=>{
	gsap.to(mesh.rotation, {duration: 1, y: mesh.rotation.y + Math.PI/2})
  }
}; 

gui.add(parameters, 'faces', 1, 500, 1);
gui.add(parameters, 'spin');
gui.add(material, 'wireframe');
gui.addColor(material, 'color');
//==========================================
```
</details>


<details>
  <summary>TEXTURES</summary>

## TEXTURES :
https://youtu.be/T2K6WXdifGA?si=SRKetahK_71ajt8D
Textures are images that will cover the surface of geometries
Texture follow PBR (Physically Based Rendering) that uses real-life algorithms, articles: ([Physically-Based Rendering, And You Can Too! | Marmoset](https://marmoset.co/posts/physically-based-rendering-and-you-can-too/), [Basic Theory of Physically-Based Rendering | Marmoset](https://marmoset.co/posts/basic-theory-of-physically-based-rendering/))

>Textures are of many types each of different effects : 
- **Color (Albedo)** : applied on geometries
- **Alpha** : grayscale image,
	- white part is visible part,
	- black part is invisible part of image
- **Height (Displacement)** : grayscale image,
	- white means max height, 
	- black means min height, 
	- move the vertices, 
	- need enough subdivisions to move height.
- **Normal** : purple/bluish image, 
	- add details mostly regarding lights, reflection refraction according to vectors
	- normal vector directing outside of the face
	- don't need subdivisions
- **Ambient Occlusion** : grayscale image,
	- add fake shadows in cervices
	- not physically accurate
- **Metalness** : grayscale image,
	- white is metallic
	- black is non metalic
	- mostly for reflection
- **Roughness** : grayscale image,
	- white is rough
	- black is smooth
	- mostly for light dissipation
	- mostly used with metalness

> How to load Textures (TextureLoader) :
```javascript
const loadingManager = new THREE.LoadingManager();

loadingManager.onStart = ()=>{
  console.log('onStart');
}
loadingManager.onLoad = ()=>{
  console.log('onLoad');
}
loadingManager.onProgress = ()=>{
  console.log('onProgress');
}
loadingManager.onError = ()=>{
  console.log('onError');
}

const textureLoader = new THREE.TextureLoader(loadingManager);

const colorTexture = textureLoader.load('/static/textures/door/color.jpg');
const metalnessTexture = textureLoader.load('/static/textures/door/metalness.jpg');
const roughnessTexture = textureLoader.load('/static/textures/door/roughness.jpg');

const material = new THREE.MeshBasicMaterial({
  map : colorTexture,
})
```

> UV Unwrapping :

Texture is being stretched and squeezed in different ways to cover different geometries, this is called UV Unwrapping. It's like unwrapping an origami, like how a cube can be unwrapped into a '+' symbol.
```javascript
console.log(geometry.attributes.uv);
```
Custom geometry would require custom uv unwrapping.

> Transform textures :
- repeat : a `Vector2` with x & y values
	```javascript
	colorTexture.repeat.x = 2; // texture cover 1/2 of the x
	colorTexture.repeat.y = 3; // texture cover 1/3 of the y
	// by default the rest part is stretcted
	// but we can change it by :
	colorTexture.wrapS = THREE.RepeatWrapping;
	colorTexture.wrapT = THREE.RepeatWrapping;
	// we can alternate (mirror) this wrapping by : 
	colorTexture.wrapS = THREE.MirroredRepeatWrapping;
	colorTexture.wrapT = THREE.MirroredRepeatWrapping;
	```
- rotation : rotate by radians
	```javascript
	colorTexture.rotation = Math.PI / 4;
	```
- offset : defines the position of the texture on the surface.
	```javascript
	colorTexture.offset.x = 0.5;
	colorTexture.offset.y = 0.5;
	```
- center : sets the pivot point for transformations (like rotation or scaling).
	```javascript
	colorTexture.center.x = 0.5;
	colorTexture.center.y = 0.5;
	```

> Mip Mapping (***Expensive***) (done by Three.js) : A technic that consist of creating half a smaller version of textures again and again till it forms a 1x1 form of texture. All those versions of textures are sent to GPU and then GPU decides which texture to use according to lighting distance angle etc..
> 
> Algorithms used in Mip Mapping are :
- Minification filter : When texture is too big for the surface, example when we zoom out then we use minified version created in Mip Mapping.
	``` javascript
	colorTexture.minFilter = THREE.NearestFilter;
	```
- Magnification filter : When texture is too big for the surface, example when we zoom out then we use minified version created in Mip Mapping.
	``` javascript
	colorTexture.magFilter = THREE.NearestFilter;
	```
> using NearestFilter is better than default as results are better and Mip Maps are not formed in this filter. Therefore when using NearestFilter disable the mipmapping generation :
```javascript
colorTexture.generateMipmaps = false;
```

> Texture Formats and Optimization : 
- weight : users will have to download the textures. [TinyPNG](https://tinypng.com/) for compression
	- `.jpg` : compression therefore lighter and better
	- `.png` : no compression therefore heavier
	- `basis` : very high compression good for GPU's
- size : images dimensions should be of power of 2, as we generate mip maps
- data : normal, alpha and color carry a lot of important details that affect the texture so we normally use `.png` format for them as it is lossless.

> Websites to find Texture :
- [Poliigon - PBR Textures, Models and HDRIs](https://www.poliigon.com/)
- [3D TEXTURES | Free seamless PBR textures and Stylized textures with Color, Normal, Displacement, Occlusion and Roughness Maps.](https://3dtextures.me/)
- [Arroway Textures - Professional Textures](https://www.arroway-textures.ch/)
- [edify-3d Model by Shutterstock | NVIDIA NIM](https://build.nvidia.com/shutterstock/edify-3d)

</details>


<details>
  <summary>MATERIALS</summary>
	
## MATERIALS : 
Materials are used to put color on each visible pixel of geometries. The algorithm used to put color are written in program called **Shaders**.
- `MeshBasicMaterial` : 
	```javascript
	// ==> map property of MeshBasicMaterial:
	const material = new THREE.MeshBasicMaterial({
	  map : minecraftTexture,
	})
	// this can also be written as :
	const material = new THREE.MeshBasicMaterial();
	material.map = minecraftTexture;


	// ==> color property of MeshBasicMaterial:
	const material = new THREE.MeshBasicMaterial({color : 'red'})
	// this can also be written as :
	const material = new THREE.MeshBasicMaterial();
	material.color = new THREE.Color('hex OR rgb(...) OR text');
	// we can combine map and color


	// ==> wireframe property of material:
	const material = new THREE.MeshBasicMaterial();
	material.wireframe = true;


	// ==> opacity property of material:
	material.transparent = true;
	material.opacity = 0.5;


	// ==> alphaMap property of MeshBasicMaterial:
	const material = new THREE.MeshBasicMaterial();
	material.map = colorTexture;
	material.transparent = true;
	material.alphaMap = alphaTexture;

	// ==> side property of material:
	// decides which side is visible
	// THREE.FrontSide (default)
	// THREE.BackSide
	// THREE.DoubleSide (more calculations therefore expensive for GPU)
	material.side = THREE.DoubleSide;
	```
	
- `MeshNormalMaterial` : 
	```javascript
	const material = new THREE.MeshNormalMaterial();
	// wireframe, transparent, opacity, side works as in MeshBasicMaterial
	// obviously map, alphaMap, color don't work.

	// ==> flatShading property of MeshNormalMaterial
	// it flatten the faces, meaning the normals won't be 
	// interpolated between the vertices
	material.flatShading = true;
	```
	
- `MeshMatcapMaterial` : 
	```javascript
	const material = new THREE.MeshMatcapMaterial()
	// displays a color by using normals with respect to camera as reference to pick the right color on a texture
	material.matcap = matcapTexture; 
	```
	Where to find matcap materials : [nidorx/matcaps: Huge library of matcap PNG textures organized by color](https://github.com/nidorx/matcaps)
	
- `MeshDepthMaterial` :
	```javascript
	const material = new THREE.MeshDepthMaterial();
	// color geometries white if they are close to near of camera and black if its close to far of camera
	```
	
- `MeshLambertMaterial` : 
	reacts with light therefore we need lights for this material
	```javascript
	// ====================== Lights =======================
	    const ambientLight = new THREE.AmbientLight(new THREE.Color('white'), 0.5);
	    scene.add(ambientLight);
	
	    const pointLight = new THREE.PointLight(0xffffff , 100);
	    pointLight.position.x = 5;
	    pointLight.position.y = 5;
	    pointLight.position.z = 5;
	    scene.add(pointLight);
	// =====================================================

	const material = new THREE.MeshLambertMaterial();
	// doesn't have reflection of light
	```
	
- `MeshPhongMaterial` : 
	reacts with light therefore we need lights for this material
	```javascript
	// ====================== Lights =======================
	    const ambientLight = new THREE.AmbientLight(new THREE.Color('white'), 0.5);
	    scene.add(ambientLight);
	
	    const pointLight = new THREE.PointLight(0xffffff , 100);
	    pointLight.position.x = 5;
	    pointLight.position.y = 5;
	    pointLight.position.z = 5;
	    scene.add(pointLight);
	// =====================================================

	const material = new THREE.MeshPhongMaterial();
	// have reflection of light
	// We can control light reflection with shininess and color of reflection with specular
	material.shininess = 500;
	material.specular = new THREE.Color('blue');
	```
	
- `MeshToonMaterial` :
	reacts with light therefore we need lights for this material
	```javascript
	// ====================== Lights =======================
	    const ambientLight = new THREE.AmbientLight(new THREE.Color('white'), 0.5);
	    scene.add(ambientLight);
	
	    const pointLight = new THREE.PointLight(0xffffff , 100);
	    pointLight.position.x = 5;
	    pointLight.position.y = 5;
	    pointLight.position.z = 5;
	    scene.add(pointLight);
	// =====================================================

	const material = new THREE.MeshToonMaterial();
	// cartoonist reflection
	// we can add a gradient to the lighting on the surface of geometries
	material.gradientMap = gradientTexture;
	// if we apply gradientMap we would loose our cartoonist effect and would have a uniform gradient(like in MeshLambertMaterial) because gradient is too small so the default magFilter i.e Linear take smaller versions of gradient texture and try to fix it therefore set magFilter to NearestFilter
	material.generateMipmaps = false;
	gradientTexture.magFilter = THREE.NearestFilter;
	gradientTexture.minFilter = THREE.NearestFilter;
	```
	
-  **(Important)** `MeshStandardMaterial` :
	reacts with light therefore we need lights for this material
	```javascript
	// ====================== Lights =======================
	    const ambientLight = new THREE.AmbientLight(new THREE.Color('white'), 0.5);
	    scene.add(ambientLight);
	
	    const pointLight = new THREE.PointLight(0xffffff , 100);
	    pointLight.position.x = 5;
	    pointLight.position.y = 5;
	    pointLight.position.z = 5;
	    scene.add(pointLight);
	// =====================================================

	const material = new THREE.MeshStandardMaterial();
	// uses PBR principals to render realistic lights
	// supports metalness and roughness
	material.metalness = 0.5;
	material.roughness = 0.2;
	//supports maps, colors etc..
	material.map = colorTexture;
	material.transparent = true;
	material.alphaMap = alphaTexture;

	// supports Ambient Occlusion maps (aoMap) which will add shadow where the texture is dark BUT we must first add uv coordinates of those dark areas
	// add a second set of UV named uv2
	plane.geometry.setAttribute(
	  'uv2',
	  new THREE.BufferAttribute(plane.geometry.attributes.uv.array, 2)
	);
	material.aoMap = ambientOcclusionTexture;
	material.aoMapIntensity = 1.5;

	// supports displacementMap
	material.displacementMap = heightTexture;
	// BUT here as plane has not enough vertices it won't be affected and sphere and torus etc.. with more vertices will change but as height map is not for them we get a weird shape
	// increase subdivisons on each geometry
	const sphere = new THREE.Mesh(
	  new THREE.SphereGeometry(0.5,64,64),
	  material
	);
	
	const plane = new THREE.Mesh(
	  new THREE.PlaneGeometry(1,1,100,100),
	  material
	);
	
	const torus = new THREE.Mesh(
	  new THREE.TorusGeometry(0.3,0.2,64,128),
	  material
	);

	// now the displacement intensity is too strong so reduce it by :
	material.displacementScale = 0.06;

	// metalness and roughness map
	material.metalnessMap = metalnessTexture;
	material.roughnessMap = roughnessTexture;

	// normal map to add how light interact reflect and refraction from a  surface of geometies
	material.normalMap = normalTexture;
	material.normalScale.set(1,1);
	```
	
- `MeshPhysicalMaterial` : 
	similar as `MeshStandardMaterial` but with more realistic and `clear coat effect`
	
- `PointsMaterial` :
	
- `ShaderMaterial and RawShaderMaterial` :
	create out own Materials

> Environment Maps
```javascript
// to load a cube texture environment we need CubeTextureLoader
const cubeTextureLoader = new THREE.CubeTextureLoader(loadingManager);

// the order in which the pngs are loaded is important
const environmentMapTexture = cubeTextureLoader.load([
  '/static/textures/environmentMap/0/px.png',
  '/static/textures/environmentMap/0/nx.png',
  '/static/textures/environmentMap/0/py.png',
  '/static/textures/environmentMap/0/ny.png',
  '/static/textures/environmentMap/0/pz.png',
  '/static/textures/environmentMap/0/nz.png',
]);

const material = new THREE.MeshStandardMaterial();
material.metalness = 0.7;
material.roughness = 0.2;
material.envMap = environmentMapTexture;
```
> To get more Environment Maps 
> 	1. [HDRIs • Poly Haven](https://polyhaven.com/hdris?ref=hdri-haven) download a hdri file of map
> 	2. [HDRI to CubeMap](https://matheowis.github.io/HDRI-to-CubeMap/) convert hdri to images

</details>


  
</details>
