# Section 2: Basics & Core Concepts - DOM Interaction with Vue

Table Content

```
├── 13. Module Introduction
├── 14. Creating and Connecting Vue App Instances
├── 15. Interpolation and Data Binding
├── 16. Binding Attributes with the "v-bind" Directive
├── 17. Understanding "methods" in Vue Apps
├── 18. Working with Data inside of a Vue App
├── 19. Outputting Raw HTML Content with v-html
├── 20. A First Summary
├── 21. Understanding Event Binding
├── 22. Events & Methods
├── 23. Working with Event Arguments
├── 24. Using the Native Event Object
├── 25. Exploring Event Modifiers
├── 26. Locking Content with v-once
├── (*) 27. Data Binding + Event Binding = Two-Way Binding
├── 28. Methods used for Data Binding: How It Works
├── 29. Introducing Computed Properties
├── 30. Working with Watchers
├── 31. Methods vs Computed Properties vs Watchers
├── 32. v-bind and v-on Shorthands
├── 33. Dynamic Styling with Inline Styles
├── 34. Adding CSS Classes Dynamically
├── 35. Classes & Computed Properties
├── 36. Dynamic Classes: Array Syntax
├── 37. Module Summary
```

## 13. Module Introduction

> Vue + HTML = Templates

## 14. Creating and Connecting Vue App Instances

## 16. Binding Attributes with the "v-bind" Directive

> v-bind: truyền các thuộc tính

Bạn không thể truyền `<a href="{{ vueLink }}">` mà cần sử dụng binding syntax

```html
<a v-bind:href="vueLink" >
```
v-bind sau đó có thể là bất cứ gì, nhưng thường sẽ là các thuộc tính của html

## 17. Understanding "methods" in Vue Apps
```js
const app = Vue.createApp({
  ...
  methods: {}
});
```
Các methods cho phép bạn xác định các hàm sẽ thực thi khi có điều gì đó xảy ra khi bạn gọi chúng chẳng hạn hoặc như bạn sẽ tìm hiểu sau, khi một sự kiện người dùng như một lần bấm nút xảy ra.

```js
const app = Vue.createApp({
  ...
  methods: {
    outputGoal() {
      const randomNumber = Math.random();
      
      if (randomNumber < 0.5) {
          return 'Learn Vue!';
      } else {
          return 'Master Vue!';
      }
    }
  }
});
```

Sử dụng
```js
<p>{{ outputGoal() }}</p>
```

## 18. Working with Data inside of a Vue App

Cú pháp this thôi: `this.courseGoalA`


## 19. Outputting Raw HTML Content with v-html
```html
<p v-html="courseGoalA"></p> // courseGoalA = "<h1> Hello, I am Minh </h1>"
```
## [20. A First Summary](https://github.com/minhnv2306/vue-pet/commit/af3b0039aee49dbf4876953b781dc3f0b6a4d24c)

## [21. Understanding Event Binding](https://github.com/minhnv2306/vue-pet/commit/852e5b48f99efd97f575226139b9c06a6ddf7bcb)

```js
v-on:click="counter++"
```

## [24. Using the Native Event Object](https://github.com/minhnv2306/vue-pet/commit/58b52ff9740f04ad3cdbeb1ac2397c2c59ac680a)

```js
<input type="text" v-on:input="setName">

methods: {
  setName(event) {
    this.name = event.target.value;
  }
}
```

## 25. Exploring Event Modifiers
Chặn nhập form
```html
<form v-on:submit.prevent="submitForm">
```
Tương tự với sự kiện click chuột phải, trái =))
```html
<button v-on:click.right="reducer(5)">

v-on:keyup.enter
```

## 26. Locking Content with v-once
`v-once:` chỉ cập nhật nội dung HTML 1 lần

## [(\*) 27. Data Binding + Event Binding = Two-Way Binding](https://github.com/minhnv2306/vue-pet/commit/30f60bc0d2a02d95857679c75bf3d30738504aa2)

Data Binding + Event Binding
```html
<input type="text" v-bind:value="name" v-on:input="setName">
```

Viết ngắn lại Two-Way Binding
```html
<input type="text" v-model="name" >
```

## 28. Methods used for Data Binding: How It Works
## [29. Introducing Computed Properties](https://github.com/minhnv2306/vue-pet/commit/5025a8390d014df2e74e3a806dd7b636cdec933d)

Khi có các thuộc tính được tính toán (ví dụ fullName tính từ name) chúng ta không dùng các methods như 28 vì ảnh hưởng đến hiệu năng. Thay vào đó, sẽ dùng computed properties
```js
computed: {
  fullname() {
    console.log("Running again....");
    return this.name + ' ' + 'Ming';
  }
}
```
Sử dụng
```html
<p> Your Name: {{ fullname }} </p>
```

Khi đó nhấn các button thì các hàm trong methods bị chạy lại, computed thì không! => Giải quyết bài toán hiệu năng

Các thuộc tính trong computed chỉ thay đổi khi thuộc tính phụ thuộc thay đổi `(this.name)`

## [30. Working with Watchers](https://github.com/minhnv2306/vue-pet/commit/e44c492795cc2126fe0c0bc0c5fb73b67565e50e)

Về cơ bản, watcher là một hàm mà bạn có thể yêu cầu Vue thực thi, khi một trong các phụ thuộc của nó thay đổi.

Được rồi, điều đó nghe giống như thuộc tính được tính toán, phải không?

Chà, thực sự bạn có thể sử dụng Watchers thay vì các thuộc tính được tính toán và đây là cách hoạt động và lý do tại sao bạn có thể không muốn làm điều đó.
```js
watch: {
  name(value) {
    // Không return gì ở đây cả, logic thôi
    this.fullname = value + ' ' + 'Ming';
  }
}
```

> Bất cứ khi nào **name** thay đổi, phương thức watcher này sẽ thực thi lại và điều đó thực sự quan trọng.  **Name** ở đây đang được sử dụng ở đây thiết lập kết nối này.
>
> Đó là cách những **watcher** hoạt động.

Bây giờ thêm 1 biến lastName nữa, và fullName = name + lastName

Khi đó watcher sẽ cần nhân đôi code
```js
watch: {
  name(value) {
    // Không return gì ở đây cả, logic thôi
    this.fullname = value + ' ' + 'Ming';
  },
  lastName(value) {
    // Không return gì ở đây cả, logic thôi
    this.fullname = this.name + ' ' + lastName;
  }
}
```

Trong khi dùng computed thì chỉ cần sửa ít code hơn
```js
computed: {
  fullname() {
    return this.name + ' ' + this.lastName;
  }
}
```

Bởi vì điều này hoạt động nhưng nó không phải là kịch bản chính để sử dụng watcher. Những watcher rất mạnh mẽ, nếu bạn có ý định khác.

Hãy quay trở lại quầy của chúng tôi ở đây. Giả sử khi bộ đếm vượt quá 50, bất cứ điều gì tương tự, chúng tôi muốn đặt lại nó. Đó là loại nhiệm vụ mà watcher tỏa sáng.
=> Kiểu hiểu xử lý 1 trường, dùng để validate :D

## 31. Methods vs Computed Properties vs Watchers

| Methods | Computed | Watch |
| -------- | -------- | -------- |
| Use with event binding OR data binding     | Use with data binding     | Not used directly in template     |
| Data binding: Method is executed for every "re-render" cycle of the component     | Computed properties are onlly re-evaluated if one of their "used values" changed     | Allows you to run any code in reaction to some changed data (e.g send HTTP request etc.     |
| Use for events or data that really needs to be re-evaluated all the time     | Use for data that depends on other data     |Use for any non-data update you want to make   |

## [32. v-bind and v-on Shorthands](https://github.com/minhnv2306/vue-pet/commit/3c006905bdac7750d46cea0cc294dc8fa1c1729c)

```js
v-on:click => @click
v-bink:value => :value
```

## [33. Dynamic Styling with Inline Styles](https://github.com/minhnv2306/vue-pet/commit/8a53ff03f505c4a4c3d10b3e1f4d7b020016e29c)

```html
<div :style="{borderColor: boxASelected ? 'red' : '#ccc'}" />
```

## [34. Adding CSS Classes Dynamically](https://github.com/minhnv2306/vue-pet/commit/e568245e342220b4e3801459d0e14ff5532146d5)
```html
<div :class="boxASelected ? 'demo active' : 'demo'" />

# Hoặc Vue hỗ trợ dạng object nhìn khá đẹp
<div :class="{demo: true, active: boxASelected}" />

# Với những class tĩnh, có thể viết luôn vào class
<div class="demo" :class="{active: boxASelected}" />
```

## 35. Classes & Computed Properties
Có thể move các class ra computed
```js
computed: {
  boxAClasses() {
    return {
      active: boxASelected
    };
  }
}
```

## [36. Dynamic Classes: Array Syntax](https://github.com/minhnv2306/vue-pet/commit/52a76f01d503e285dae5ca5fb85fa95334bfc34d)
Bạn cũng có thể viết class từ cú pháp mảng, tùy vào sở thích cá nhân =))

```html
<div :class="['demo', {active: boxASelected}]"></div>
```

## 37. Module Summary
