# Section 13: Routing


Table Content

```
├── 165. Module Introduction
├── 166. What & Why?
├── 167. Routing Setup
├── 168. Registering & Rendering Routes
├── 169. Navigating with router-link
├── 170. Styling Active Links
├── 171. Programmatic Navigation
├── 172. Passing Data with Route Params (Dynamic Segments)
├── 173. Navigation & Dynamic Paths
├── 174. A Vue Bug
├── 175. Updating Params Data with Watchers
├── 176. Passing Params as Props
├── 177. Redirecting & "Catch All" Routes
├── 178. Using Nested Routes
├── 179. More Fun with Named Routes & Location Objects
├── 180. Using Query Params
├── 181. Rendering Multiple Routes with Named Router Views
├── 182. Controlling Scroll Behavior
├── 183. Introducing Navigation Guards
├── 184. Diving Deeper Into Navigation Guards
├── 185. The Global "afterEach" Guard
├── 186. Beyond Entering: Route Leave Guards
├── 187. Utilizing Route Metadata
├── 188. Organizing Route Files
├── 189. Summary
├── 190. Module Resources
```

## 165. Module Introduction

## [167. Routing Setup](https://github.com/minhnv2306/vue-pet/commit/7a15a916e19cca51eb5f0bb2ca2c229d0030d049)
```sh
npm install --save vue-router@next
```
Tiếp tục thêm router
```js
// main.js

import { createRouter, createWebHistory } from 'vue-router';

const router = createRouter({
  history: createWebHistory(),
  routers: [
    { path: '/teams', component: TeamsList },
    { path: '/users', component: UsersList },
  ]
});

const app = createApp(App);

app.use(router);
```
Và trong App.vue
```html
<main>
  <router-view></router-view>
</main>
```

## [168. Registering & Rendering Routes](https://github.com/minhnv2306/vue-pet/commit/3827c8d90a592ce3089043ebc89036754a537fb4)

## [169. Navigating with router-link](https://github.com/minhnv2306/vue-pet/commit/a24f72be866cbc180c8a615c3521cb25f35fcbed)
```html
<ul>
  <li>
    <router-link to="/teams">Teams</router-link>
  </li>
</ul>
```

## [170. Styling Active Links](https://github.com/minhnv2306/vue-pet/commit/b8577b0d525071c354c6be9de4f8751756f771c1)

## 171. Programmatic Navigation
```js
methods: {
  comfirmInput() {
    // do something
    this.$router.push('/teams'); // move đến /teams
    this.$router.back();
    this.$router.forward();
  }
}
```

## 172. Passing Data with Route Params (Dynamic Segments)
## [173. Navigation & Dynamic Paths](https://github.com/minhnv2306/vue-pet/commit/fc15ef3000f88229fdb90f6af6330e96ff0a831b)
## 174. A Vue Bug
## [175. Updating Params Data with Watchers](https://github.com/minhnv2306/vue-pet/commit/ae65f34594fd3e04f23bf55e222428f70d85e303)
## [176. Passing Params as Props](https://github.com/minhnv2306/vue-pet/commit/da807df49593da4bdaacd96b533382d8b0a515d9)
## [177. Redirecting & "Catch All" Routes](https://github.com/minhnv2306/vue-pet/commit/5b87ee40dda2d1f50be056bd67302fd79ed61802)
## 178. Using Nested Routes
Sủ dụng tùy chọn childrent trong routers
```js
routers: [
  { path: '/teams', component: TeamsList, childrent: [
    { path: ':teamId', component: TeamMembers, props: true }, // /teams/t1
  ]}
]
```

## [179. More Fun with Named Routes & Location Objects](https://github.com/minhnv2306/vue-pet/commit/9c741874fa2a9c3991a4785ac7f395ae1f09e0d8)
- Có thể đặt name cho router (như Laravel luôn)

## [180. Using Query Params](https://github.com/minhnv2306/vue-pet/commit/ccc37fcc9cf8a1d1320d3b7dafb5daee2a282827)
## [181. Rendering Multiple Routes with Named Router Views](https://github.com/minhnv2306/vue-pet/commit/c8f309e57512cc6dee6ee554801e47f9de365a03)
## [182. Controlling Scroll Behavior](https://github.com/minhnv2306/vue-pet/commit/3c523c2997f6345b52cc161cc348f27d86293d5c)
## 183. Introducing Navigation Guards
## 184. Diving Deeper Into Navigation Guards
## 185. The Global "afterEach" Guard
## [186. Beyond Entering: Route Leave Guards](https://github.com/minhnv2306/vue-pet/commit/4ba954df208c37c2715d000bddcf13ea344c8cca)
## 187. Utilizing Route Metadata
## [188. Organizing Route Files](https://github.com/minhnv2306/vue-pet/commit/5c40ba9399f7617a82b645d27279876683b9a52a)

```
├── /pages
├── /components
├── App.vue
├── main.js
├── router.js
```
