<script>
import { nextTick } from "vue";

export default {
  data() {
    return {
      tempText: "tempText",
      tempBool: true,
      count: 1,
      author: {
        name: "John Doe",
        books: [
          "Vue 2 - Advanced Guide",
          "Vue 3 - Basic Guide",
          "Vue 4 - The Mystery",
        ],
      },
      isActive: true,
      awesome: true,
      items: [{ message: "Foo" }, { message: "Bar" }],
      name: "Vue.js",
    };
  },
  methods: {
    increment() {
      this.count++;
      nextTick(() => {
        console.log(this.count);
      });
    },
    greet(event) {
      // `this`는 메서드가 활성화된 현재 인스턴스를 가리킵니다.
      alert(`안녕 ${this.name}!`);
      // 'event'는 네이티브 DOM 이벤트 객체입니다.
      if (event) {
        alert(event.target.tagName);
      }
    },
    warn(message, event) {
      // 이제 네이티브 이벤트 객체에 접근할 수 있습니다.
      if (event) {
        event.preventDefault();
      }
      alert(message);
    },
  },
  computed: {
    publishedBooksMessage() {
      return this.author.books.length > 0 ? "Yes" : "No";
    },
  },

  mounted() {
    console.log(this.count);
    this.increment();
    console.log(this.count);
  },
};
</script>

<template>
  <h1>this is test page.</h1>
  <h2>
    <span>{{ tempText }}</span>
    <br />
    <span>{{ tempBool ? "진실" : "거짓" }}</span>
    <p v-if="tempBool">보이나요?</p>
    <p>{{ count }}</p>
  </h2>

  <button @click="increment">Count</button>

  <div :class="{ active: isActive }">
    <p>책을 가지고 있다!</p>
    <span>{{ publishedBooksMessage }}</span>
  </div>
  <div>
    <button @click="awesome = !awesome">전환</button>

    <h1 v-if="awesome">Vue는 정말 멋지죠!</h1>
    <h1 v-else>아닌가요? 😢</h1>
  </div>
  <div>
    <li v-for="item in items">
      {{ item.message }}
    </li>
  </div>
  <div>
    <button @click="greet">환영하기</button>
    <button @click="warn('아직 양식을 제출할 수 없습니다.', $event)">
      제출하기
    </button>
  </div>
</template>
