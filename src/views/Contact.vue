<template>
  <div class="contact">
    <h1>Contact</h1>
    <TransitionGroup tag="ul" appear @before-enter="beforeEnter" @enter="enter">
      <li v-for="(icon, index) in icons" :key="icon.name" :data-index="index">
        <span class="material-icons">{{ icon.name }}</span>
        <div>{{ icon.text }}</div>
      </li>
    </TransitionGroup>
  </div>
</template>

<script>
import { ref } from "vue";
import gsap from "gsap";

export default {
  setup() {
    const icons = ref([
      { name: "alternate_email", text: "by email" },
      { name: "local_phone", text: "by phone" },
      { name: "local_post_office", text: "by post" },
      { name: "local_fire_department", text: "by smoke signal" },
    ]);

    const beforeEnter = (el) => {
      el.style.transform = "translateY(80px)";
      el.style.opacity = 0;
    };

    const enter = (el, done) => {
      gsap.to(el, {
        y: 0,
        duration: 0.8,
        opacity: 1,
        delay: el.dataset.index * 0.2,
        onComplete: done,
      });
    };

    return { icons, beforeEnter, enter };
  },
};
</script>

<style>
.contact ul {
  padding: 0;
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-gap: 20px;
  max-width: 400px;
  margin: 60px auto;
}
.contact li {
  list-style-type: none;
  background: white;
  padding: 30px;
  border-radius: 10px;
  box-shadow: 1px 3px 5px rgba(0, 0, 0, 0.1);
  cursor: pointer;
  line-height: 1.5em;
}
</style>
