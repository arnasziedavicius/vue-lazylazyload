# Vue-LazyLazy-Load

- Real simple image preloading to be used with Vue.js
- Goes with both img tag and background-image property
- JavaScript ES6 compatible

(☞ ͡° ͜ʖ ͡°)☞

## Setup

### Registration

Register a global custom *lazy* directive where Vue.js is defined.

```
Vue.directive('lazy', (el, binding) => {
  const img = new Image();

  img.src = binding.value;
  img.onload = () => {
    if (binding.arg) {
      el.setAttribute('style', `${binding.arg}: url(${binding.value})`);
    } else {
      el.setAttribute('src', binding.value);
    }
    el.setAttribute('lazy', 'loaded');
  };

  img.onerror = (e) => {
    console.log(e);
  };
});
```

### Usage

Img tag:

```
<img 
  src="./your-placeholder-image.jpg" 
  v-lazy="image.src" 
  lazy />
```

Background-image:

```
  <div 
    :style="{ 'background-image' : 'url(./your-placeholder-image.jpg)' }"
    v-lazy:background-image="image.src"
    lazy></div>
```

### Styling

Styling example with a nice fade-in effect:

```
[lazy] {
  opacity: 0;
  visibility: hidden;
  -webkit-transition: opacity .2s ease, visibility .2s ease;
  transition: opacity .2s ease, visibility .2s ease;
}
[lazy='loaded'] {
  opacity: 1;
  visibility: visible;
}
```
