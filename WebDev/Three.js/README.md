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




## LOOK AT THIS ! 
```javascript
	// lookAt() is used to look at something
	camera.lookAt( new THREE.Vector3(0,0,0) );
	camera.lookAt( mesh.position );
```




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


  
</details>
