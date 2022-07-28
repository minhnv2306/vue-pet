# Section 9: Diving Deeper Into Components

Table Content

```
├── 108. Module Introduction
├── 109. Project Setup
├── 110. Global vs Local Components
├── 111. Scoped Styles
├── 112. Introducing Slots
├── 113. Named Slots
├── 114. Slot Styles & Compilation
├── 115. More on Slots
├── 116. Scoped Slots
├── 117. Dynamic Components
├── 118. Keeping Dynamic Components Alive
├── 119. Applying What We Know & A Problem
├── 120. Teleporting Elements (Dịch chuyển Elements) 
├── 121. Working with Fragments
├── 122. The Vue Style Guide
├── 123. Moving to a Different Folder Structure
├── 124. Modeule Summary
```

## 108. Module Introduction
## 109. Project Setup
## 110. Global vs Local Components
> Global Components: Components you can **use anywhere** in your Vue app - i.e. in **any template**

Cấu trúc các component, một số component không sử dụng nhiều thì không cần đặt global (như Header chỉ dùng 1 lần)

Sử dụng tùy chọn `components` đăng ký component nội bộ
```html
<!-- App.vue -->
<script>
import TheHeader from './components/TheHeader.vue';

export default {
  commponents: {
    'the-header': TheHeader
    // Or
    // TheHeader
  }
}
```

## [111. Scoped Styles](https://github.com/minhnv2306/vue-pet/commit/be5f3f117829d8ce0c7fefd48ed2bc3d856038d6)
Dùng scoped trong file để style chỉ ảnh hưởng đến phạm vi component
```html
<style scoped>
section {
  margin: 2rem auto;
}
```
Khi bạn F12 lên, bạn sẽ thấy css được sinh kèm data-v-{id} cho các component của bạn

## [112. Introducing Slots](https://github.com/minhnv2306/vue-pet/commit/27cf5b559841bc5b21af3f600ed86b42a4a86b32)
Đọc thêm thẻ base card
```html
<!-- BaseCard.vue -->
<template>
  <div>
    <slot></slot>
  </div>
</template>
```
Vì vậy, giao diện này thực sự đến từ Component của chúng tôi và đó là cách các Slot hoạt động.

Chúng cho phép chúng tôi nhận nội dung HTML cũng có thể đang sử dụng các tính năng Vue từ bên ngoài Component.

Về cơ bản giống như props nhưng ở đó props được sử dụng cho dữ liệu mà một Component cần, các Slot được sử dụng cho mã HTML cho template mà một Component cần.

## [113. Named Slots](https://github.com/minhnv2306/vue-pet/commit/0b1214dd0db1c211b362ddaabc158d97e18380d2)
Các bài toán nhiều slot cho Component. Chúng ta cần đặt tên cho slot
```html
<!-- BaseCard.vue -->
<template>
  <div>
    <header>
      <slot name="header"></slot>
    </header>
    <slot></slot>
  </div>
</template>
```

> Bạn không cần đặt tên cho toàn bộ Slot, cái không có tên sẽ là mặc định, nhưng bạn phải chỉ có một Slot chưa được đặt tên

Sau đó sử dụng slot qua `<template>` và slot cùng với tên của slot. Slot mặc định thì tự động nhận ngoài template hoặc có thể sử dụng `<template v-slot:default>`
```html
<!-- UserInfo.vue -->
<template>
  <section>
    <base-card>
      <template v-slot:header>
        <h3>{{ fullName }} <h3>
        ...
      </template>
      <template v-slot:default>
        <p>{{ infoText }}</p>
      </template>
    </base-card>
  </div>
</template>
```

## 114. Slot Styles & Compilation
Slot ở trên đã phá vỡ CSS, bây giờ cần chỉnh lại

Bạn cần di chuyển đoạn code trong Component App vào BaseCard, vì slot sẽ ở trong BaseCard.

## [115. More on Slots](https://github.com/minhnv2306/vue-pet/commit/2cef3b3f50a5f03ed5c97403ef266fde7c0a8959)
- Nội dung mặc định cho slot
```html
<slot name="header">
  <h2> The Default </h2>
</slot>
```
- Xem các slots của Component
```js
<!-- BaseCard.vue -->
export default {
  mounted() {
    console.log(this.$slots);
  }
}
```
Chỉnh sửa nội dung slot
```
// BaseCard
export default {
  mounted() {
    console.log(this.$slots.header);
  }
}
```
- Shot syntax of slot
`<template v-slot:header>` => `<template #header>`

## [116. Scoped Slots](https://github.com/minhnv2306/vue-pet/commit/3e4316979a4553a0b6bd91476928be0a288b3ba2)

Bây giờ Scoped Slots là gì?

Khái niệm về Scoped Slots là cho phép bạn truyền dữ liệu từ bên trong Component mà bạn đã xác định vị trí cho Component nơi bạn chuyển đánh dấu cho Slot đó.
```
// CourseGoalds.vue
<template>
  <ul>
    <li v-for="goal in goals" :key="goal">
      <slot :item="goal"></slot>
    </li>
  </ul>
</template>
```
Và bạn có thể truy cập. Tất cả các props của slot sẽ được truyền vào `slotProps`
```
// App.Vue
<course-goals>
  <template #default="slotProps">
    <h2>{{ slotProps.item }} <h2>
  </template>
</course-goals>
```

Và cách viết ngắn hơn =))

```
// App.Vue
<course-goals #default="slotProps">
	<h2>{{ slotProps.item }} <h2>
</course-goals>
```

## 117. Dynamic Components
Thẻ `<component>` để lựa chọn Component nào sẽ hiển thị. Bạn có thể coi nó như 1 helper để bạn tạo component động
```
<component :is="selectedComponent"></component> // tương đương <active-goal></active-goal>
```

## [118. Keeping Dynamic Components Alive](https://github.com/minhnv2306/vue-pet/commit/12f62d9de652f9429f78f9dbf000e87e5293d661)
Khi chuyển qua chuyển lại các component, component bị remove và hiện lại, do đó dữ liệu bị mất. Nếu bạn muốn giữ component động, sử dụng `<keep-alive>`
```
<keep-alive>
  <component :is="selectedComponent"></component>
</keep-alive>
```

## 119. Applying What We Know & A Problem
Một ví dụ về validate lỗi

## [120. Teleporting Elements (Dịch chuyển Elements)](https://github.com/minhnv2306/vue-pet/commit/2cf9bb4ac00344154109ddaed38ae6a8cb2970ce)
Vị trí dialog cần ở ngoài div, không phải trong div con => Cần dịch chuyển dialog ra ngoài

Bọc component bằng thẻ Teleport. Về mặt code, nó nằm trong div nhưng khi render thực sự nó ở 1 nơi khác =))
```
<teleport to="body">
  <error-alert v-if="inputIsInvalid">
    ...
  </error-alert>
</teleport>
```

> Nó không cải thiện chức năng nhưng nó làm cấu trúc HTML của bạn đẹp hơn và đúng hơn về mặt ngữ nghĩa =))

## [121. Working with Fragments](https://github.com/minhnv2306/vue-pet/commit/cf73c4c35baed4b42cb65f6a9303af45b448dd71)
Giống Fragment trong React

## 122. The Vue Style Guide

https://v2.vuejs.org/v2/style-guide/?redirect=true

## [123. Moving to a Different Folder Structure](https://github.com/minhnv2306/vue-pet/commit/5aa8ffd754149881efebe1e977be49eea3bc3cfe)

## 124. Module Summary
