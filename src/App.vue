<template>
  <div class="home">
    <img alt="Vue logo" src="./assets/logo.png" />
    <HelloWorld msg="Welcome to Your Vue.js App" />
    <button @click="toggleSideBar">我是 ElButton</button>
    <h1>{{ states.sidebar }}</h1>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";
import { mapGetters } from "vuex";
import { defineComponent, ref, reactive, computed } from "vue";
import { useStore } from "vuex";

export default defineComponent({
  name: "Home",
  components: {
    HelloWorld
  },
  setup() {
    const store = useStore();
    const { getters, dispatch /*, commit */ } = useStore();
    // console.log(dispatch("app/toggleSideBar"));
    const toggleSideBar = () => {
      dispatch("app/toggleSideBar");
    };
    // const toggleSideBar = () => {
    //   store.commit("app/TOGGLE_SIDEBAR");
    // };
    const radio1 = ref(store.state.app.sidebar);
    const states = reactive({
      sidebar: computed(() => getters.sidebar),
    });
    // console.log(getters.sidebar, states.sidebar);

    return {
      radio1,
      radio2: ref("1"),
      radio3: ref("1"),
      radio4: ref("1"),
      states,
      toggleSideBar,
    }; // 这里返回的任何内容都可以用于组件的其余部分
  },
  computed: {
    ...mapGetters(["sidebar"]),
  },
  mounted() {
    console.log(this.sidebar);
  },
});
</script>
