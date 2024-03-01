<template>
  <h1>Edit Project</h1>
  <form @submit.prevent="">
    <label>Project Title</label>
    <input type="text" v-model="title">
    <label>Project Detail</label>
    <textarea cols="30" rows="10" v-model="detail"></textarea>
    <button @click="updateProject">Update Project</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      title: "",
      detail : ""
    }
  },
  props: ['id'],
  mounted() {
    fetch('http://localhost:4000/projects/' + this.id)
      .then((res) => {
      return res.json()
      })
      .then((datas) => {
        this.title = datas.title;
        this.detail = datas.detail;
      })
      .catch((err) => {
        console.log(err);
    })
  },
  methods: {
    updateProject()
    {
      fetch('http://localhost:4000/projects/' + this.id, {
        method: "PATCH",
        headers: {
          "Content-Type" : "application/json"
        },
        body: JSON.stringify(
          {
            title: this.title,
            detail : this.detail
          }
        )
      })
        .then(() => {
          this.$router.push('/');
        })
        .catch((err) => {
          console.log(err);
      })
    }
  },
}
</script>

<style>

</style>