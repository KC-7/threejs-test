# ThreeJS Mini Test Project

This mini project is a very basic test of Three.js, a JavaScript library used for creating 3D graphics in the browser. The app showcases how to set up a simple 3D scene with a pyramid object and a background image, using basic materials and geometry. The pyramid rotates on its x and y axes. Additionally, the app includes interactivity for the pyramid object, allowing users to change its color by clicking on it.

## How To Use

You can access the live link [here](https://kc-7.github.io/threejs-test/).

Alternativly, to launch the web app from the repo:
1. Type `python3 -m "http.server"` into the terminal window. 
2. Click open in new tab to run and view the server locally.

## Technologies Used

HTML is used to scructure the web page. 

CSS is used to add basic style and responsiveness for smaller screen sizes. 

JS is used with the ThreeJS library to create the project. 

## ThreeJS

1. Creating a Scene:

    var scene = new THREE.Scene();

This creates a new Three.js scene object, which will contain all the 3D objects, lights, and cameras in the scene.

2. Creating a Camera:

var camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
This creates a new Three.js camera object, which determines the viewpoint from which the scene is rendered. The PerspectiveCamera constructor takes several parameters, including the field of view, the aspect ratio, and the near and far clipping planes.

3. Creating a Renderer:

    var renderer = new THREE.WebGLRenderer();
    renderer.setSize(window.innerWidth, window.innerHeight);
    document.body.appendChild(renderer.domElement);

This creates a new Three.js renderer object, which is responsible for rendering the scene onto the screen. The WebGLRenderer constructor is used to create a renderer that uses WebGL, a technology that allows for fast and efficient 3D rendering in a web browser. The setSize method sets the size of the renderer to match the size of the window. The domElement property is the canvas element that the renderer uses to draw the scene, which is appended to the HTML document.

4. Adding a Background Texture:

    var textureLoader = new THREE.TextureLoader();
    var backgroundTexture = textureLoader.load("imgs/bg.jpg");
    scene.background = backgroundTexture;

This loads an image file as a texture using the TextureLoader class and sets it as the background of the scene.

5. Creating a 3D Object:

    var geometry = new THREE.ConeGeometry(1, 2, 3);
    var material = new THREE.MeshBasicMaterial({
        color: 0x00ff00,
        transparent: true,
        opacity: 0.75
    });
    var pyramid = new THREE.Mesh(geometry, material);
    scene.add(pyramid);

This creates a 3D pyramid object using the ConeGeometry class, which takes the radius, height, and number of segments as parameters. A MeshBasicMaterial is used to define the appearance of the pyramid, including its color, transparency, and opacity. The Mesh class is used to combine the geometry and material into a single 3D object, which is added to the scene.

6. Positioning the Camera:

    camera.position.z = 5;

This sets the position of the camera to (0,0,5) in the scene, so that the camera is 5 units away from the origin along the z-axis.

7. Animating the Object:

    var animate = function () {
        requestAnimationFrame(animate);

        pyramid.rotation.x += 0.01;
        pyramid.rotation.y += 0.01;

        renderer.render(scene, camera);
    };
    animate();

This creates an animation loop that updates the rotation of the pyramid object every frame. The requestAnimationFrame method is used to request that the browser calls the animate function on the next available frame. Within the animate function, the rotation of the pyramid is updated and the scene is rendered using the renderer and camera objects.

8. Detecting Object Clicks:

    function onDocumentClick(event) {
        event.preventDefault();

        var mouseX = (event.clientX / window.innerWidth) * 2 - 1;
        var mouseY = -(event.clientY / window.innerHeight) * 2 + 1;

        var vector = new THREE.Vector3(mouseX, mouseY, 0.5);
   
The script adds an event listener to the document that listens for clicks. When the user clicks, the onDocumentClick function is called. This function first gets the mouse coordinates using event.clientX and event.clientY. Then, it creates a vector and unprojects it from the camera position using the unproject method of the camera object. The vector is then used to create a raycaster, which is used to detect whether the user clicked on the pyramid object.

9. Changing Object Color:

    if (intersects.length > 0) {
        // If the object is clicked, set a random color
        pyramid.material.color.setHex(Math.random() * 0xffffff);
    } else {
        // If the object is not clicked, set the color back to green
        pyramid.material.color.set(0x00ff00);
    }

If the raycaster detects an intersection with the pyramid object, the pyramid's color is set to a random color using the setHex method of the material object. If there is no intersection, the pyramid's color is set back to green.

10. Adding a Black Outline:

    // Add a black outline to the pyramid
    var edges = new THREE.EdgesGeometry(pyramid.geometry);
    var outlineMaterial = new THREE.LineBasicMaterial({
        color: 0x000000, // Set the outline color to black
    });
    var outline = new THREE.LineSegments(edges, outlineMaterial);
    pyramid.add(outline);

This script adds a black outline to the pyramid by creating a new geometry with edges, and a line segments object with the outline material. The line segments object is added to the pyramid using the add method. This gives the pyramid a visual outline that helps to differentiate it from the background.

11. Starting the Animation Loop: 

   // Start the animation loop
    animate();

This code starts the animate function as outlined in step 7 above.

## Credits

- [Background Image by exnico](https://www.freepik.com/free-vector/psychedelic-colorful-eyes-seamless-pattern_27839654.htm#query=trippy%20seamless%20pattern&position=2&from_view=search&track=robertav1) on Freepik.

- I got the ThreeJS Library file and learned how to it up on [ThreeJS.org](https://threejs.org/docs/index.html#manual/en/introduction/Creating-a-scene).

- The coding for this project was created using the above resouce alongside the assitance of ChatGPT to add additional functionality and create parts of the readme. 
