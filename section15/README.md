# Section 15

Table Content

```
├── 210. Module Introduction
├── 211. What & Why?
├── 212. Creating & Using a Store
├── 213. Connecting Components to State
├── 214. Introducing Mutations - A Better Way of Changing Data
├── 215. Passing Data to Mutations with Payloads
├── 216. Introducing Getters - A Better Way Of Getting Data
├── 217. Running Async Code with Actions
├── 218. Understanding the Action "Context"
├── 219. Using Mapper Helpers
├── 220. Example: Adding More State
├── 221. Organizing your Store with Modules
├── 222. Understanding Local Module State
├── 223. Namespacing Modules
├── 224. Structuring Vuex Code & Files
├── 225. A Challenge!
├── 226. Challenge Solution (1/3)
├── 227. Challenge Solution (2/3)
├── 228. Challenge Solution (3/3)
├── 229. Summary
```
**Better State Management with VueX**

Replacing provider/inject

> VueX is a library for managing global state(thông tin user đang đăng nhập, cart item)

## 212. Creating & Using a Store
```sh
npm install --save vuex@next
```
Thêm store trong file main.js
```js
import { createStore } from 'vuex';

const store = createStore({
  state() {
    return {
      counter: 0
    }
  }
});

...
app.use(store);
```
Và sử dụng App.vue
```html
<h3>{{ $store.state }}</h3>
```

## [213. Connecting Components to State](https://github.com/minhnv2306/vue-pet/commit/86445cb7f438c7dfc634178dd252043a13fc0aaa)
```js
methods: {
  addOne() {
    this.$store.state.counter++;
  }
}
```

## 214. Introducing Mutations - A Better Way of Changing Data

## [215. Passing Data to Mutations with Payloads](https://github.com/minhnv2306/vue-pet/commit/f00cab94f0f359087f86f140f5b0bd0c1ba6f466)

## [216. Introducing Getters - A Better Way Of Getting Data](https://github.com/minhnv2306/vue-pet/commit/2d903ace04e189d611b6f35152e3df0a95498243)

## [217. Running Async Code with Actions](https://github.com/minhnv2306/vue-pet/commit/3ea7412cf825cdd8d78bb09760e499b354e1d758)

## 218. Understanding the Action "Context"

## [219. Using Mapper Helpers](https://github.com/minhnv2306/vue-pet/commit/2667b9d621a6c71277e7c3a223bf95945b994a5a)

## [220. Example: Adding More State](https://github.com/minhnv2306/vue-pet/commit/0b4be27142658994dc42ef0f8003596539007695)

## [221. Organizing your Store with Modules](https://github.com/minhnv2306/vue-pet/commit/56a6dab3b9d70383093fbdf2210d6c7d9be4c059)

## 222. Understanding Local Module State

## [223. Namespacing Modules](https://github.com/minhnv2306/vue-pet/commit/c2d711b909252e96d726d120f730b692aea78ce1)

## [224. Structuring Vuex Code & Files](https://github.com/minhnv2306/vue-pet/commit/bda9aed2d935f1cd48c1b39902a54fb7d9bce3d1)

## [225. A Challenge!](https://github.com/minhnv2306/vue-pet/commit/a1b5b7d22425a6a1b8e279b3517bada4cfec4225)

## [226. Challenge Solution (1/3)](https://github.com/minhnv2306/vue-pet/commit/00ba182543060655a5b5bcc42c8cd30607525c03)

## [227. Challenge Solution (2/3)](https://github.com/minhnv2306/vue-pet/commit/ce8f024282d4dbc1a108ba0980f9c44df6832b27)

## [228. Challenge Solution (3/3)](https://github.com/minhnv2306/vue-pet/commit/6f91f607f36a7313a7d9a26ee592524a1eeb76c5)

## 229. Summary
