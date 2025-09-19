<template>
  <div ref="container" class="absolute inset-0 z-0"></div>
</template>

<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount } from 'vue';
import * as THREE from 'three';

const container = ref<HTMLElement | null>(null);
let scene: THREE.Scene;
let camera: THREE.PerspectiveCamera;
let renderer: THREE.WebGLRenderer;
let points: THREE.Points;
let connections: THREE.LineSegments;
let frameId: number;

interface Node {
  position: THREE.Vector3;
  connections: number[];
}

const init = () => {
  if (!container.value) return;

  // Scene setup
  scene = new THREE.Scene();
  camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
  renderer = new THREE.WebGLRenderer({ alpha: true });
  renderer.setSize(window.innerWidth, window.innerHeight);
  container.value.appendChild(renderer.domElement);

  // Create neural network
  const nodes: Node[] = [];
  const nodeCount = 50;
  const maxConnections = 3;

  // Create nodes
  for (let i = 0; i < nodeCount; i++) {
    nodes.push({
      position: new THREE.Vector3(
        (Math.random() - 0.5) * 100,
        (Math.random() - 0.5) * 100,
        (Math.random() - 0.5) * 50
      ),
      connections: []
    });
  }

  // Create connections
  for (let i = 0; i < nodes.length; i++) {
    const connectionCount = Math.floor(Math.random() * maxConnections) + 1;
    for (let j = 0; j < connectionCount; j++) {
      const target = Math.floor(Math.random() * nodes.length);
      if (target !== i && !nodes[i].connections.includes(target)) {
        nodes[i].connections.push(target);
      }
    }
  }

  // Create points geometry
  const pointsGeometry = new THREE.BufferGeometry();
  const pointsPositions = new Float32Array(nodeCount * 3);
  const pointsSizes = new Float32Array(nodeCount);

  nodes.forEach((node, i) => {
    pointsPositions[i * 3] = node.position.x;
    pointsPositions[i * 3 + 1] = node.position.y;
    pointsPositions[i * 3 + 2] = node.position.z;
    pointsSizes[i] = Math.random() * 2 + 1;
  });

  pointsGeometry.setAttribute('position', new THREE.BufferAttribute(pointsPositions, 3));
  pointsGeometry.setAttribute('size', new THREE.BufferAttribute(pointsSizes, 1));

  const pointsMaterial = new THREE.PointsMaterial({
    color: 0x4a90e2,
    size: 1,
    transparent: true,
    opacity: 0.8,
    sizeAttenuation: true
  });

  points = new THREE.Points(pointsGeometry, pointsMaterial);
  scene.add(points);

  // Create connections geometry
  const linePositions: number[] = [];
  nodes.forEach((node, i) => {
    node.connections.forEach(targetIndex => {
      linePositions.push(node.position.x, node.position.y, node.position.z);
      linePositions.push(
        nodes[targetIndex].position.x,
        nodes[targetIndex].position.y,
        nodes[targetIndex].position.z
      );
    });
  });

  const linesGeometry = new THREE.BufferGeometry();
  linesGeometry.setAttribute('position', new THREE.Float32BufferAttribute(linePositions, 3));

  const linesMaterial = new THREE.LineBasicMaterial({
    color: 0x4a90e2,
    transparent: true,
    opacity: 0.3
  });

  connections = new THREE.LineSegments(linesGeometry, linesMaterial);
  scene.add(connections);

  camera.position.z = 100;
};

const animate = () => {
  frameId = requestAnimationFrame(animate);

  if (points && connections) {
    points.rotation.x += 0.001;
    points.rotation.y += 0.001;
    connections.rotation.x += 0.001;
    connections.rotation.y += 0.001;

    // Pulse effect for points
    const sizes = points.geometry.attributes.size;
    for (let i = 0; i < sizes.count; i++) {
      sizes.array[i] = Math.sin(Date.now() * 0.001 + i) + 2;
    }
    sizes.needsUpdate = true;
  }

  renderer.render(scene, camera);
};

const handleResize = () => {
  if (!container.value) return;

  camera.aspect = window.innerWidth / window.innerHeight;
  camera.updateProjectionMatrix();
  renderer.setSize(window.innerWidth, window.innerHeight);
};

onMounted(() => {
  if (typeof window !== 'undefined') {
    init();
    animate();
    window.addEventListener('resize', handleResize);
  }
});

onBeforeUnmount(() => {
  if (typeof window !== 'undefined') {
    cancelAnimationFrame(frameId);
    window.removeEventListener('resize', handleResize);
    if (container.value) {
      container.value.removeChild(renderer.domElement);
    }
  }
});
</script>