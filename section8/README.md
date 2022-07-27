# Section 8: Component Communication

Table Content

```
├── 91. Module Introduction
├── 92. Introducing "Props" (Parent => Child Communication)
├── 93. Prop Behavior & Changing Props
├── 94. Validating Props
├── 95. Supported Prop Values
├── 96. Working with Dynamic Prop Values
├── 97. Emitting Custom Events (Child => Parent Communication)
├── 98. Defining & Validating Custom Events
├── 99. Prop / Event Fallthrough & Binding All Props
├── 100. Demo: Adding Components & Connecting Them
├── 101. Demo: Adding More Component Communication
├── 102. A Potential Problem
├── 103. Provide + Inject To The Rescue
├── 104. Provide + Inject for Functions / Methods
├── 105. Provide + Inject vs Props & Custom Events
├── 106. Module Summary
```

## [92. Introducing "Props" (Parent => Child Communication)](https://github.com/minhnv2306/vue-pet/commit/0604d5e95d5e6f9b3ff7b287383d18fd804c107e)
```js
<friend-contact
    name="Manuel Lorenz"
    phone-number="01234 56789"
></friend-contact>
```
Trong component
```js
export default {
    props: [
        'name',
        'phoneNumber'
    ],
    ...
}
```
> Vue sẽ tự hiểu phone-number về phoneNumber

## 93. Prop Behavior & Changing Props
## [94. Validating Props](https://github.com/minhnv2306/vue-pet/commit/cf18dcec513a1a93c93bde66fc2bc8c54743934a)
## [96. Working with Dynamic Prop Values](https://github.com/minhnv2306/vue-pet/commit/19cf8844d0fb189427abe2479959a5058f4f92bf)
## [97. Emitting Custom Events (Child => Parent Communication)](https://github.com/minhnv2306/vue-pet/commit/8320c5348969a0435dd51516096dd0d0ae4123da)
> emit: con truyền sự kiện lên cha
```js
// FriendContact.Vue
methods: {
    toggleFavorite() {
        this.$emit('toggle-favorite', this.id);
    }
}
```
Nghe sự kiện trên cha
```js
// App.Vue
<friend-contact
    ...
    @toggle-favorite="toggleFavoriteStatus"
></friend-contact>

...
methods: {
    toggleFavoriteStatus(friendId) {
        ...
    }
}
```

## [98. Defining & Validating Custom Events](https://github.com/minhnv2306/vue-pet/commit/bd35b304ccde5be9cfa98941066e2bcf2c5f3f3e)
Tiếp theo chúng ta tiến thêm 1 bước viết code gọn gàng hơn nứa cho emit
```js
...
emits: [
    'toggle-favorite'
],
```
Có thể xử lý luôn với tùy chọn này
```js
emits: {
    'toggle-favorite': function(id) {
        // Validate ID and process in here
    }
},
```

## [100. Demo: Adding Components & Connecting Them](https://github.com/minhnv2306/vue-pet/commit/89b4eaa2c67a0f46f320a8b081d4ce9ca83f754a)

> Nên đọc code đoạn này để hiểu hơn

## 101. Demo: Adding More Component Communication

## [102. A Potential Problem](https://github.com/minhnv2306/vue-pet/commit/352dd9c0b755918ce1525137232925b220590d93)
> Nên đọc code đoạn này để hiểu hơn

Đang có vấn đề trong đoạn code, sẽ xử ý trong 103+104+105

## 103. Provide + Inject To The Rescue
```js
provide: {
    topics: [
        ...
    ]
}

export default {
    inject: ['topics'],
}
```
Và đây là một lưu ý quan trọng, bạn chỉ có thể tiêm những gì đã được cung cấp ở cấp cao hơn.

Về cơ bản, có nghĩa là, trong một thành phần mẹ hoặc một thành phần tổ tiên của KnowledgeGrid.

Ví dụ: nếu chúng tôi cung cấp một cái gì đó trong ActiveElement, chúng tôi không thể đưa nó vào KnowledgeGrid. Vì vậy, bạn không thể Provide + Inject giữa những người hàng xóm

Viết ngắn lại
```js
provide() {
    return {
        topics: this.topics
    };
}
```
Vì vậy, bằng chứng này Provide + Inject hoạt động.

Bây giờ, Provide + Inject mẫu rất hữu ích nếu bạn muốn tránh các thành phần chuyển qua và các Component chuyển qua không cần thiết.

## [104. Provide + Inject for Functions / Methods](https://github.com/minhnv2306/vue-pet/commit/541795c9e9a2f1278782421bd4f265f1f98c3574)
Ngoài ra inject cũng có thể áp dụng cho Functions và Methods

## 105. Provide + Inject vs Props & Custom Events

Provide + Inject => Giao tiếp cha con và bản chất không thể thay thế props and events
Provide + Inject giúp viết ít code hơn ^^ nhưng cũng có con dao 2 lưỡi, khiến code khó đọc hơn khi phải vào Component xem dữ liệu là gì? Nó có thể khó khăn hơn với các ứng dụng phức tạp :'(

## 106. Module Summary
