<!DOCTYPE html>
<html>
<head>
  <title>Kunal's 3D Avatar</title>
  <style>
    body {
      margin: 0;
      background: #121212;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      color: white;
      font-family: sans-serif;
    }
    canvas {
      display: block;
    }
  </style>
</head>
<body>
  <script src="https://cdn.jsdelivr.net/npm/three@0.132.2/build/three.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/three@0.132.2/examples/js/controls/OrbitControls.js"></script>
  
  <script>
    const scene = new THREE.Scene();

    // Camera
    const camera = new THREE.PerspectiveCamera(
      75,
      window.innerWidth / window.innerHeight,
      0.1,
      1000
    );
    camera.position.z = 5;

    // Renderer
    const renderer = new THREE.WebGLRenderer({ antialias: true });
    renderer.setSize(window.innerWidth, window.innerHeight);
    document.body.appendChild(renderer.domElement);

    // Lighting
    const ambientLight = new THREE.AmbientLight(0xffffff, 0.6);
    scene.add(ambientLight);
    const directionalLight = new THREE.DirectionalLight(0xffffff, 1);
    directionalLight.position.set(2, 2, 5);
    scene.add(directionalLight);

    // Orbit Controls
    const controls = new THREE.OrbitControls(camera, renderer.domElement);

    // Avatar Group
    const avatar = new THREE.Group();

    // Head
    const headGeometry = new THREE.SphereGeometry(1, 32, 32);
    const headMaterial = new THREE.MeshPhongMaterial({ color: 0xffcc99 });
    const head = new THREE.Mesh(headGeometry, headMaterial);
    avatar.add(head);

    // Glasses
    const glassMaterial = new THREE.MeshPhongMaterial({ color: 0x333333 });
    const leftGlass = new THREE.Mesh(
      new THREE.TorusGeometry(0.5, 0.05, 16, 100),
      glassMaterial
    );
    leftGlass.position.set(-0.35, 0.1, 0.7);
    leftGlass.rotation.y = Math.PI / 2;
    avatar.add(leftGlass);

    const rightGlass = leftGlass.clone();
    rightGlass.position.x = 0.35;
    avatar.add(rightGlass);

    // Body
    const bodyGeometry = new THREE.CylinderGeometry(0.7, 1, 2, 32);
    const bodyMaterial = new THREE.MeshPhongMaterial({ color: 0x2196f3 });
    const body = new THREE.Mesh(bodyGeometry, bodyMaterial);
    body.position.y = -1.7;
    avatar.add(body);

    scene.add(avatar);

    // Responsive Resize
    window.addEventListener("resize", () => {
      camera.aspect = window.innerWidth / window.innerHeight;
      camera.updateProjectionMatrix();
      renderer.setSize(window.innerWidth, window.innerHeight);
    });

    // Animation
    function animate() {
      requestAnimationFrame(animate);
      avatar.rotation.y += 0.01;
      controls.update();
      renderer.render(scene, camera);
    }
    animate();
  </script>
</body>
</html>
