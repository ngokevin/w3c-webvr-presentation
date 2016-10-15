<!-- .slide: data-background="media/img/aframe.png" -->

<div class="talk-title">
  <h1>A-Frame</h1>
  <p>A web framework for building VR experiences</p>
  <p class="talk-info">
    @andgokevin | Mozilla VR | aframe.io
  </p>
</div>

<!-- NOTES -->
- Easy for web developers to create VR content
- Prototype WebVR and VR UX faster
- Create a thriving ecosystem around WebVR

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
- Add HTML elements that represent 3D primitives
- Readable: HTML arguably most accessible language in computing
- Declarative: visual representation of scene graph, fully represents state
- Encapsulated: copy-and-paste HTML anywhere else and still work, no state or variables
- Quickly look at a live example...

------

## Hello Metaverse

<!-- .slide: data-transition="none" data-state="state--bg-dark" -->

<div class="stretch" data-aframe-scene="scenes/80s.html"></div>

<!-- NOTES -->
- A-Frame scene by Ada Rose Edwards running from inside my HTML slides
- Works on desktop, Android, iOS, Samsung Gear VR, Oculus Rift, HTC Vive
- *Action:* View source in DOM inspector and change text value live

------

## Works With Everything Under the Sun

- React
- d3.js
- jQuery
- Vue.js
- Angular
- Mustache / Handlebars / Nunjucks / Jade / Underscore / EJS
- Ember.js
- Meteor.js
- Mithril

- Since just HTML, compatible with all existing libraries/frameworks: $/d3/Vue/React/Angular
- HTML is a sturdy bridge between WebGL and everything else
- Super easy to learn. Can do a lot with simple HTML elements, but to create compelling VR experiences, we need more power...

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
- What does this look like in A-Frame...

------

<!-- .slide: data-background="media/img/minecraft-blocks.png" data-transition="slide-in none" -->

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

## Composing an Entity

<!-- .slide: data-background="media/img/minecraft-blocks.png" data-transition="none" -->

```html
<a-entity
  geometry="primitive: sphere; radius: 1.5"
  material="color: #343434; roughness: 0.4; sphericalEnvMap: #texture">
```
<!-- .element: class="stretch" -->

------

## Composing an Entity

<!-- .slide: data-background="media/img/minecraft-blocks.png" data-transition="none" -->

```html
<a-entity
  geometry="primitive: sphere; radius: 1.5"
  material="color: #343434; roughness: 0.4; sphericalEnvMap: #texture"
  position="-1 2 4" rotation="45 0 90" scale="2 2 2">
```
<!-- .element: class="stretch" -->

------

## Composing an Entity

<!-- .slide: data-background="media/img/minecraft-blocks.png" data-transition="none" -->

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

## Composing an Entity

<!-- .slide: data-background="media/img/minecraft-blocks.png" data-transition="none" -->

```html
<a-entity
  json-model="src: #robot"
  position="-1 2 4" rotation="45 0 90" scale="2 2 2"
  animation="property: rotation; loop: true; to: 0 360 0"
  movement-pattern="type: spline; speed: 4">
```
<!-- .element: class="stretch" -->

------

## Composing an Entity

<!-- .slide: data-background="media/img/minecraft-blocks.png" data-transition="none" -->

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

<!-- .slide: data-background="media/img/minecraft-blocks.png" data-transition="none" -->

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
- Can do anything within a component (full access to three.js, JavaScript, APIs) can get
  exposed declaratively
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

<!-- .slide: data-background="media/img/aframe-side.png" -->

Curated collection of A-Frame components/shaders.

<a class="stretch" href="https://aframe.io/aframe-registry">
  <video loop data-src="media/video/registrypreview.mp4" data-autoplay></video>
</a>

------

## Angle

<!-- .slide: data-background="media/img/aframe-side.png" -->

<img data-src="media/img/angle.png" width="300">

A-Frame CLI. Install components into HTML files.

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

Visual tool for A-Frame. Just `<ctrl>+<alt>+i`.

<div class="stretch" data-aframe-scene="scenes/80s.html"></div>

------

## aframe-react

<img data-src="media/img/aframe-react.jpg" width="240">

```js
import 'aframe';
import 'aframe-animation-component';
import 'aframe-bmfont-text-component';
import {Entity, Scene} from 'aframe-react';
import React from 'react';
import ReactDOM from 'react-dom';

class VRScene extends React.Component {
  render () {
    return (
      <Scene>
        <Entity id="box"
          geometry={{primitive: 'box'}}
          material="color: red" position="0 0 -5"
          onClick={() => {console.log('Clicked!');}}/>

        <Entity id="text"
          animation={{property: "rotation"; loop: true; to: "0 360 0"}}
          bmfont-text={{text: 'Hello World!'}}
          position="0 1 -5"/>
      </Scene>
    );
  }
}
```

------

## A-Frame Mixin Style Sheets

```css
red { material { color: #393E51; } }
white { material { color: #E9E6C9; } }
blue { material { color: #566683; } }
box { geometry { primitive: box; } }
sphere { geometry { primitive: sphere; } }
spinning { animation { attribute: rotation; loop: true; to: 0 360 0 } }
```

```
<a-style src="index.mss"></a-style>
<a-entity mixin="blue sphere"></a-entity>
<a-entity mixin="spinning red box"></a-entity>
<a-entity mixin="white" text="text: I am white."></a-entity>
```

------

## Performance

- <!-- .element: class="fragment" -->  Modified `registerElement` and `HTMLElement.prototype` to remove asynchrony
- <!-- .element: class="fragment" -->  `setAttribute` synchronous + directly updates underlying `Object3D`s
- <!-- .element: class="fragment" -->  Developer-set HTML attributes cached. Run-time updates done in memory
- <!-- .element: class="fragment" -->  Disabled serialization back to DOM

------

<!-- .slide: data-background-video="media/video/a-painter.mp4" data-background-video-muted data-state="state--bg-dark" -->

## A-Painter

Paint in VR in the browser.

------

<!-- .slide: data-background="media/img/a-painter-logo.jpg" data-state="state--bg-dark" -->

## A-Painter

Share VR paintings with just links.

<iframe class="stretch" data-src="https://aframe.io/a-painter/?url=https://ucarecdn.com/962b242b-87a9-422c-b730-febdc470f203/"></iframe>

------

<!-- .slide: data-background="media/img/a-shooter-concept.jpg" -->

## A-Shooter

<video class="stretch" data-src="media/video/a-shooter.mp4" data-autoplay loop muted
  style="opacity: 0.95">

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
