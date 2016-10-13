<!-- .slide: data-background="media/img/aframe-rendered-full.png" -->

<div class="talk-title">
  <h1>A-Frame</h1>
  <p>A web framework for building VR experiences</p>
  <p class="talk-info">
    @andgokevin | Mozilla VR | aframe.io
  </p>
</div>

<!-- NOTES -->
- Easy for web developers to create VR content, without graphics knowledge
- Prototype and experiment WebVR and VR UX faster
- Vehicle to kickstart WebVR ecosystem

------

## Hello World

<!-- .slide: data-transition="slide-in none" -->

```html
<html>
  <script src="https://aframe.io/releases/0.3.2/aframe.min.js"></script>
  <a-scene>





  </a-scene>
</html>
```
<!-- .element: class="stretch" -->

<!-- NOTES -->
- Explain boilerplate `<a-scene>` handles

------

## Hello World

<!-- .slide: data-transition="fade-in slide-out" -->

```html
<html>
  <script src="https://aframe.io/releases/0.3.2/aframe.min.js"></script>
  <a-scene>
    <a-box color="#4CC3D9" position="-1 0.5 -3" rotation="0 45 0"></a-box>
    <a-cylinder color="#FFC65D" position="1 0.75 -3" radius="0.5" height="1.5"></a-cylinder>
    <a-sphere color="#EF2D5E" position="0 1.25 -5" radius="1.25"></a-sphere>
    <a-plane color="#7BC8A4" position="0 0 -4" rotation="-90 0 0" width="4" height="4"></a-plane>
    <a-sky color="#ECECEC"></a-sky>
  </a-scene>
</html>
```
<!-- .element: class="stretch" -->

<!-- NOTES -->
- Simple HTML markup for a basic scene
- Remember to manipulate on second display
- Readable: HTML arguably most accessible language in computing
- Declarative: visual representation of scene graph, fully represents state
- Encapsulated: copy-and-paste HTML anywhere else and still work, no variables

------

## Hello World

<!-- .slide: data-transition="none" -->

<div class="stretch" data-aframe-scene="scenes/hello-world.html"></div>

------

## Hello Metaverse

<!-- .slide: data-transition="none" -->

<div class="stretch" data-aframe-scene="scenes/80s.html"></div>

<!-- NOTES -->
- As web technology, we can embed within slides
- Can view this in desktop, Android, iOS, Samsung Gear VR, Oculus Rift, HTC Vive
- View source in DOM inspector and change values live
- Based on DOM, compatible with all libraries/frameworks: d3.js, Vue.js, React

------

```html
<a-animation> <a-box> <a-camera> <a-circle> <a-collada-model>
<a-cone> <a-cursor> <a-curvedimage> <a-cylinder>
<a-dodecahedron> <a-isocahedron> <a-image> <a-light>
<a-obj-model> <a-plane> <a-ring> <a-tetrahedron> <a-torus>
<a-torus-knot> <a-sky> <a-sound> <a-sphere> <a-videosphere>
```

<!-- NOTES -->
- Handful elements that ship with A-Frame, but this is just the start
- Pretty easy to get a WebVR scene up and running

------

# Entity-Component-System

<!-- .slide: data-background="media/img/minecraft-blocks.png" -->

<!-- NOTES -->
- Pattern popular in game development, used in game engines like Unity
- All objects in scene are **entities** that inherently empty objects. Plug in
  **components** to attach appearance / behavior / functionality
- Favors composition over inheritance
- Minecraft analogy: all blocks are entities, mix-and-match components to
  create different kinds of blocks (appearance, physics, behavior, sound, strength)

------

<!-- .slide: data-background="media/img/entity-component-system.png" data-background-size="contain" data-state="state--bg-white" -->

<!-- NOTES -->
- Additional analogies: smartphone, vehicle
- AFAIK A-Frame first tool to make ECS declarative

------

<!-- .slide: data-transition="slide-in none" -->

## Composing an Entity

```html
<a-entity>
```
<!-- .element: class="stretch" -->

<!-- NOTES -->
- Start with an `<a-entity>`
- By itself, has no appearance, behavior, functionality
- Plug in components to add appearance, behavior, functionality

------

<!-- .slide: data-transition="fade-in none" -->

## Composing an Entity

```html
<a-entity
  geometry="primitive: sphere; radius: 1.5"
  material="color: #343434; roughness: 0.4; sphericalEnvMap: #texture">
```
<!-- .element: class="stretch" -->

------

<!-- .slide: data-transition="fade-in none" -->

## Composing an Entity

```html
<a-entity
  geometry="primitive: sphere; radius: 1.5"
  material="color: #343434; roughness: 0.4; sphericalEnvMap: #texture"
  position="-1 2 4" rotation="45 0 90" scale="2 2 2">
```
<!-- .element: class="stretch" -->

------

<!-- .slide: data-transition="fade-in none" -->

## Composing an Entity

```html
<a-entity
  geometry="primitive: sphere; radius: 1.5"
  material="color: #343434; roughness: 0.4; sphericalEnvMap: #texture"
  position="-1 2 4" rotation="45 0 90" scale="2 2 2"
  animation="property: rotation; loop: true; to: 0 360 0"
  movement-pattern="type: spline; speed: 4">
```
<!-- .element: class="stretch" -->

------

<!-- .slide: data-transition="fade-in none" -->

## Composing an Entity

```html
<a-entity
  json-model="src: #robot"
  position="-1 2 4" rotation="45 0 90" scale="2 2 2"
  animation="property: rotation; loop: true; to: 0 360 0"
  movement-pattern="type: spline; speed: 4">
```
<!-- .element: class="stretch" -->

------

<!-- .slide: data-transition="fade-in none" -->

## Composing an Entity

```html
<a-entity
  json-model="src: #robot"
  position="-1 2 4" rotation="45 0 90" scale="2 2 2"
  animation="property: rotation; loop: true; to: 0 360 0"
  movement-pattern="type: attack; target: #player"
  explode="on: hit">
```
<!-- .element: class="stretch" -->

------

## Registering a Component

```js
AFRAME.registerComponent('mycomponent', {
  schema: {
    foo: {type: 'selector'},
    bar: {default: 256}
  },

  init: function () { // ... },
  update: function () { // ... },
  remove: function () { // ... },
  tick: function () { // ... },
  pause: function () { // ... },
  play: function () { // ... }
});
```
<!-- .element: class="stretch" -->

```html
<a-box mycomponent="foo: #box; bar: 300"></a-box>
```

<!-- NOTES -->
- `schema`: defines how data is parsed from HTML
- Lifecycle methods:
  - `init`: component attached, like `componentDidMount`
  - `update`: component data update, like `componentWillReceiveProps`
  - `remove`: component detached, like `componentWillUnmount`
  - `tick`: run on every frame
- Properties:
  - `el`: reference to entity element
  - `data`: component data parsed from HTML
  - `object3D`: three.js object

------

<!-- .slide: data-background="media/img/standard-components.png" data-background-size="contain" -->

<!-- NOTES -->
- Components that ship with A-Frame
- Bare bones, allow ecosystem to enable features

------

<!-- .slide: data-background="media/img/community-components.png" data-background-size="contain" -->

<!-- NOTES -->
- Components built by the community and ecosystem
- Developers enabling others
- Components can be consumed without programming knowledge

------

## Registry

Curated collection of A-Frame components and shaders.

<a class="stretch" href="https://aframe.io/aframe-registry">
  <video loop src="media/video/registrypreview.mp4" autoplay></video>
</a>

------

## Angle

<img src="media/img/angle.png" width="300">

CLI to install components from Registry into HTML files.

```bash
npm install -g angle
angle createapp
angle install aframe-physics-system
angle install mountain
angle install ocean
angle install particle-system
```

------

## Inspector

------

<!-- .slide: data-background="media/img/360syria.jpg" -->

## Fear of the Sky

Amnesty International UK

[360syria.com](http://360syria.com)

<!-- NOTES -->
- Journalism, e-commerce, and real estate popular production use cases

------

## Stand at the Edge of Geologic Time

<!-- .slide: data-background="media/img/npr.png" -->

National Public Radio (NPR)

[apps.npr.org/rockymountain-vr](http://apps.npr.org/rockymountain-vr/)

------

<!-- .slide: data-background="media/img/mars.jpg" -->

## Journey to Mars

The Washington Post

[washingtonpost.com/video/mars/public/](https://www.washingtonpost.com/video/mars/public/)

------

<!-- .slide: data-background-video="media/video/livetour.mp4" data-background-video-loop="true" -->

## LiveTour

iStaging

[vrviewer.istaging.co/#!/684173](http://vrviewer.istaging.co/#!/684173)

<!-- NOTES -->
- Virtual real estate and apartment tours

------

# Augmented Reality

<video class="stretch" data-src="media/video/argon.mp4" data-autoplay loop></video>

<!-- NOTES -->
- Not just a framework for VR, can also handle 3D and AR as well
- Prototype by Blair MacIntyre from Georgia Tech with Argon Browser
- Most predict AR to be even bigger market than VR

------

# aframe.io

<div class="captioned-image-row">
  <div>
    <img data-src="media/img/github.png">
    <i>75 contributors 3500 Stargazers</i>
  </div>
  <div>
    <img data-src="media/img/slack.png">
    <i>1700 members on Slack</i>
  </div>
  <div>
    <img data-src="media/img/scene-collage-circle.png">
    <i>100s of featured projects</i>
  </div>
</div>

<!-- NOTES -->
- Open source and inclusive project
- Most work done on GitHub
- Active community on Slack to share projects, interact, hang out, seek help
- Featured projects on the `awesome-aframe` repository and *A Week of A-Frame* blog
