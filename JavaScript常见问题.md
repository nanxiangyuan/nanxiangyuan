## js 里面的 ?? 和 || 的区别


- 1. ** `||` 的行为: 遇到 falsy 就用右边的值 **

```js
0 || 10                 // → 10      (0 是 falsy)
"" || "default"         // → "default" (空字符串是 falsy)
false || true           // → true    (false 是 falsy)
null || "abc"           // → "abc"
undefined || "abc"      // → "abc"
NaN || 1                // → 1
```

- 2. ** `??` 的行为: 只有在遇到 `null` 或者是 `undefined` 才用右边的值 **

```js
0 ?? 10                 // → 0       ✅ 保留 0
"" ?? "default"         // → ""      ✅ 保留空字符串
false ?? true           // → false   ✅ 保留 false
null ?? "abc"           // → "abc"
undefined ?? "abc"      // → "abc"
NaN ?? 1                // → NaN
```

## Typescript 里面 interface 和 type 的区别

- `interface` 用于定义对象的形状;
    - 不支持基础类型的定义
    - 在 OOP 语言里面可以被类实现 (implements)
    - 可以使用 extends 关键字实现继承;
    - 可以重复定义;
- `type` 用于创建类型别名, 可以给任意类型取一个名字, 包括原始类型, 联合类型, 元组, 对象等;
    - 支持基础类型定义;
    - 不可以被重复定义;


## react 里面的 useMemo, useCallback hook 的作用以及用法

- `useMemo` 用于缓存计算结果, 避免在每次渲染时都进行昂贵的计算;
    - 第一个参数为一个函数, 返回需要缓存的值;
    - 第二个参数为依赖数组, 只有当依赖项变化时, 才会重新计算;
- `useCallback` 用于缓存函数本身, 避免函数在每次渲染时重新创建;
    - 返回一个记忆化的函数;
    - 只有当依赖项变化时, 才会返回新的函数实例;
    - 主要用于传递给子组件的回调函数, 防止子组件因父组件重新渲染而不必要的重新渲染;




## Threejs 

Three.js 的核心是利用 WebGL 在浏览器中渲染 3D 图形, WebGL 是基于 OpenGL ES 的 JavaScript API, 直接调用 GPU 进行图形渲染; Three.js 在其基础上提供了高级抽象, 简化了开发流程;

### Threejs 核心组件:

- Scene(场景):
    - 所有 3D 对象的容器, 相当于一个“舞台”;
    - 包含模型、灯光、相机等;
- Camera(相机):
    - 定义观察视角, 决定“从哪里看”场景;
    - 常见类型: PerspectiveCamera (透视相机) 、OrthographicCamera(正交相机);
- Renderer(渲染器):
    - 负责将场景和相机渲染到 `<canvas>` 元素上;
    - 使用 WebGL 渲染器 (WebGLRenderer) 与 GPU 通信
- Mesh(网格):
    - 由 Geometry (几何体) 和 Material (材质) 组成
    - 几何体定义形状(如立方体、球体), 材质定义外观(颜色、纹理、光照响应)
- Light(灯光):
    - 模拟真实光照效果, 如 DirectionalLight、PointLight、AmbientLight 等
- Animation Loop(动画循环):
    - 使用 requestAnimationFrame 实现持续更新和渲染;


### Three.js 渲染流程

1. 初始化阶段

```js
// 创建场景
const scene = new THREE.Scene();

// 创建相机
const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
camera.position.z = 5;

// 创建渲染器
const renderer = new THREE.WebGLRenderer();
renderer.setSize(window.innerWidth, window.innerHeight);
document.body.appendChild(renderer.domElement);

// 创建物体
const geometry = new THREE.BoxGeometry();
const material = new THREE.MeshBasicMaterial({ color: 0x00ff00 });
const cube = new THREE.Mesh(geometry, material);
scene.add(cube);
```

2. 渲染循环

```js
function animate() {
    requestAnimationFrame(animate);

    // 更新逻辑 (如旋转)
    cube.rotation.x += 0.01;
    cube.rotation.y += 0.01;

    // 渲染场景
    renderer.render(scene, camera);
}
animate();
```

3. 底层渲染流程

- 场景遍历
- 模型矩阵计算
- 视图矩阵与投影矩阵
- GPU 渲染管线
- 输出到 Canvas


## Threejs 和 WebGL 的关系

- WebGL 是浏览器提供的底层图形 API, 基于 OpenGL ES, 直接操作 GPU;
- Three.js 是 WebGL 的高级封装库, 提供了更易用的面向对象 API, 隐藏了着色器编写、缓冲区管理等复杂细节;


## Three.js 中的渲染循环是如何工作的

使用 requestAnimationFrame 实现一个递归函数, 每一帧: 

- 更新对象状态 (如位置、旋转)
- 调用 renderer.render(scene, camera) 重新渲染场景确保动画流畅 (通常 60 FPS)


## 如何优化 Three.js 的性能

- 使用 BufferGeometry 替代 Geometry (更高效)
- 合并几何体 (BufferGeometryUtils.mergeBufferGeometries)
- 使用实例化渲染 (InstancedMesh)渲染大量相同物体
- 控制渲染频率 (非动画时暂停渲染)
- 减少材质数量, 复用材质
- 使用 LOD (Level of Detail) 控制远近模型精度
- 开启 frustum culling (视锥剔除)
- 压缩纹理, 使用合适尺寸


## Three.js 中的材质 (Material) 有哪些常见类型？区别是什么

- MeshBasicMaterial: 基础材质, 不受光照影响;
- MeshLambertMaterial: 漫反射材质, 支持简单光照;
- MeshPhongMaterial: 支持高光反射;
- MeshStandardMaterial: PBR 材质, 基于物理渲染, 最真实;
- MeshNormalMaterial: 显示法线方向, 用于调试;


## 什么是着色器 (Shader) ？Three.js 如何使用自定义着色器？

- 着色器是运行在 GPU 上的小程序, 分为顶点着色器和片元着色器.
- Three.js 支持通过 ShaderMaterial 或 RawShaderMaterial 自定义着色器:

```js
const material = new THREE.ShaderMaterial({
    vertexShader: document.getElementById('vertexShader').textContent,
    fragmentShader: document.getElementById('fragmentShader').textContent
});
```

## 如何处理 Three.js 中的内存泄漏

- 销毁不再使用的对象;
- 移除事件监听器;
- 清理 TextureLoader、GLTFLoader 等加载器缓存;
- 避免在动画循环中重复创建对象;
















