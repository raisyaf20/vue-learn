<template>
  <section>
    <div class="container">
      <h2>Framework / Library</h2>
      <p>Selesai {{ completed }}</p>
      <button @click="showForm = !showForm">Add Framewrok | Library</button>
      <div v-show="showForm">
        <form class="flex col mt" @submit.prevent="onSubmit">
          <label for="title">Name Framework or library</label>
          <input type="text" name="title" id="title" />
          <label for="desc">Description</label>
          <input type="text" name="desc" id="desc" />
          <div class="btn-flex">
            <button type="submit" class="btn">Submit</button>
            <button type="reset" class="btn">reset</button>
          </div>
        </form>
      </div>
      <div class="flex mt">
        <div
          class="card"
          :class="{ check: el.state }"
          v-for="el in lists"
          :key="el.title"
        >
          <h3>{{ el.title }}</h3>
          <p>{{ el.desc }}</p>
          <input
            type="checkbox"
            name="check"
            :checked="el.state"
            @change="el.state = !el.state"
          />
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      showForm: false,
      lists: [
        {
          title: "Vue",
          desc: "learn vue",
          state: false,
        },
        {
          title: "Angular",
          desc: "learn angular",
          state: false,
        },
      ],
    };
  },
  computed: {
    completed() {
      return this.lists.filter((e) => e.state == true).length;
    },
  },
  methods: {
    onSubmit(val) {
      const x = val.target.elements;
      const tit = x.title.value;
      const desc = x.desc.value;
      this.lists.push({
        title: tit,
        desc: desc,
      });
      alert(`Success Add ${tit}`);
      this.showForm = false;
    },
  },
};
</script>

<style>
body {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin: 0;
  padding: 0;
}
.container {
  max-width: 1250px;
  margin: 10px auto;
  padding: 0.9rem;
}
.flex {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 1.3rem;
}
.card {
  background: #eaeaea;
  width: 18rem;
  padding: 0.85rem;
  border-radius: 15px;
  box-shadow: 2px 2px 5px rgba(0, 0, 0, 0.45);
}
.check {
  background: rgb(13, 224, 66);
}
.col {
  width: 250px;
  flex-direction: column;
}
.mt {
  margin-top: 40px;
}
.btn-flex {
  display: flex;
  justify-content: center;
}
.btn {
  padding: 0.55rem 1.5rem 0.55rem 1.5rem;
  margin-right: 10px;
  border-radius: 15px;
  border: none;
  background: salmon;
}
</style>
