<!-- .slide: data-background="media/img/aframe.jpg" -->

<div class="talk-title">
  <h1>A-Frame</h1>
  <p>A web framework for building VR experiences</p>
  <p class="talk-info">
    @andgokevin | Mozilla VR | aframe.io
  </p>
</div>

<!-- NOTES -->
- On-board for web developers to creating VR content, otherwise 3D intimidating.
- Prototype WebVR experiences faster
- Kickstart a content ecosystem on top of WebVR to push the platform
- Become the most popular way to produce WebVR content today

------

## Hello World

<!-- .slide: data-background="media/img/aframe.png" data-transition="slide-in none" -->

```html
<html>
  <script src="https://aframe.io/releases/0.3.2/aframe.min.js"></script>
  <a-scene>





  </a-scene>
</html>
```
<!-- .element: class="stretch" -->

<!-- NOTES -->
- Just a plain HTML file, no need to install anything or build steps
- Using Custom Elements, `<a-scene>` handles tons 3D and WebVR boilerplate alone
  - Canvas, camera, renderer, lights, controls, render loop
  - WebVR polyfill, VREffect
- Put stuff inside our scene...

------

## Hello World

<!-- .slide: data-background="media/img/aframe.png" data-transition="fade-in slide-out" -->

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
- Basic 3D primitives with Custom Elements
- Readable: HTML arguably most accessible language in computing
- Encapsulated: copy-and-paste HTML anywhere else and still work, no state or variables
- Quickly look at a live example...

------

## Hello Metaverse

<!-- .slide: data-transition="none" data-state="state--bg-dark" -->

<div class="stretch" data-aframe-scene="scenes/80s.html"></div>

<!-- NOTES -->
- A-Frame scene by Ada Rose Edwards running from inside my HTML slides
- Works on desktop, Android, iOS, Samsung Gear VR, Oculus Rift, HTC Vive
- Could open up the DOM Inspector to change values live
- Since it's just HTML...

------

<!-- .slide: data-background="media/img/aframe.jpg" -->

## Works With Everything

<div class="captioned-image-row">
  <div>
    <img data-src="media/img/d3.png">
    <i>d3.js</i>
  </div>
  <div>
    <img data-src="media/img/vue.png">
    <i>Vue.js</i>
  </div>
  <div>
    <img data-src="media/img/react.png">
    <i>React</i>
  </div>
  <div>
    <img data-src="media/img/jquery.png">
    <i>jQuery</i>
  </div>
  <div>
    <img data-src="media/img/ember.png">
    <i>Ember.js</i>
  </div>
  <div>
    <img data-src="media/img/angular.png">
    <i>Angular</i>
  </div>
</div>

<!-- NOTES -->

- Based on HTML, compatible with all existing/future libraries/frameworks: $/d3/Vue/React/Angular
- Good reason to have HTML as an intermediary layer between WebGL/three.js
- Ultimately, a declarative and extensible framework for three.js

------

# Entity-Component-System

<!-- .slide: data-background="media/img/minecraft-blocks.png" -->

<!-- NOTES -->
- At A-Frame's core is an entity-component-system pattern
- Popular in game development, used by Unity
- All objects in scene are **entities** that inherently empty objects. Plug in
  **components** to attach appearance / behavior / functionality
- Favors composition over inheritance. 3D is different, objects have complex appearance and behavior as opposed to 2D where everything is a fixed block.
- Minecraft analogy: all blocks are entities, mix-and-match components to
  create different kinds of blocks (appearance, physics, behavior, sound, strength)

------

<!-- .slide: data-background="media/img/standard-components.png" data-background-size="contain" -->

<!-- NOTES -->
- Some standard components that ship with A-Frame

------

<!-- .slide: data-background="media/img/community-components.png" data-background-size="contain" -->

<!-- NOTES -->
- Components built by the community and ecosystem
- Can have components for physics, oceans, mountains that can be dropped in as a `<script>` tag and used straight from HTML...

------

<div class="icon-title">
  <img data-src="media/img/registry.png" width="64">
  <h2>Registry</h2>
</div>

<!-- .slide: data-background="media/img/aframe-side.png" -->

Curated collection of A-Frame components/shaders.

<a class="stretch" href="https://aframe.io/aframe-registry">
  <video loop data-src="media/video/registrypreview.mp4" data-autoplay></video>
</a>

------

## Inspector

<!-- .slide: data-background="media/img/inspector.png" data-state="state--bg-dark" -->

Visual tool for A-Frame. Just `<ctrl>+<alt>+i`.

<div class="stretch" data-aframe-scene="scenes/80s.html"></div>

------

<!-- .slide: data-background-video="media/video/a-painter.mp4" data-background-video-muted="true" data-state="state--bg-dark" -->

## A-Painter

Paint in VR in the browser.

<!-- NOTES -->
- Performance
- 90+fps room-scale TiltBrush experience in a few weeks with A-Frame

------

<!-- .slide: data-background="media/img/a-painter-logo.jpg" data-state="state--bg-dark" -->

## A-Painter

Share VR paintings with just links.

<iframe class="stretch" data-src="https://aframe.io/a-painter/?url=https://ucarecdn.com/962b242b-87a9-422c-b730-febdc470f203/"></iframe>

------

# aframe.io

<div class="captioned-image-row">
  <div>
    <img data-src="media/img/github.png">
    <i>75 contributors 3500 Stargazers</i>
  </div>
  <div>
    <img data-src="media/img/slack.png">
    <i>1750 members on Slack</i>
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
