<!DOCTYPE html>
<html>
<head>
  <title>Kunal's 3D Avatar</title>
  <style>
    body { margin: 0; }
    canvas { display: block; }
  </style>
</head>
<body>
  <script src="https://cdn.jsdelivr.net/npm/three@0.132.2/build/three.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/three@0.132.2/examples/js/controls/OrbitControls.js"></script>
  
  <script>
    // Scene setup
    const scene = new THREE.Scene();
    const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
    const renderer = new THREE.WebGLRenderer({ antialias: true });
    renderer.setSize(800, 400);
    document.body.appendChild(renderer.domElement);
    
    // Lighting
    const light = new THREE.AmbientLight(0x404040);
    scene.add(light);
    const directionalLight = new THREE.DirectionalLight(0xffffff, 1);
    directionalLight.position.set(1, 1, 1);
    scene.add(directionalLight);
    
    // Create stylized avatar
    const createAvatar = () => {
      const group = new THREE.Group();
      
      // Head
      const headGeometry = new THREE.SphereGeometry(1, 32, 32);
      const headMaterial = new THREE.MeshPhongMaterial({ color: 0xffcc99 });
      const head = new THREE.Mesh(headGeometry, headMaterial);
      group.add(head);
      
      // Glasses
      const glassGeometry = new THREE.TorusGeometry(0.5, 0.05, 16, 100);
      const glassMaterial = new THREE.MeshPhongMaterial({ color: 0x333333 });
      const leftGlass = new THREE.Mesh(glassGeometry, glassMaterial);
      leftGlass.position.set(-0.35, 0.1, 0.7);
      leftGlass.rotation.y = Math.PI / 2;
      group.add(leftGlass);
      
      // ... add more avatar parts (body, arms, etc)
      
      return group;
    };
    
    const avatar = createAvatar();
    scene.add(avatar);
    camera.position.z = 5;
    
    // Animation loop
    function animate() {
      requestAnimationFrame(animate);
      avatar.rotation.y += 0.01;
      renderer.render(scene, camera);
    }
    animate();
  </script>
</body>
</html>
