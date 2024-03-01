<template>
  <h1>Add Project</h1>
  <form @submit.prevent="addProject">
    <label>Project Title</label>
    <input type="text" v-model="title">
    <label>Project Detail</label>
    <textarea cols="30" rows="10" v-model="detail"></textarea>
    <button>Add Project</button>
  </form>
</template>

<script>
export default {
data() {
  return {
    title : "",
    detail : ""
  }
  },
methods: {
  addProject()
  {
    fetch('http://localhost:4000/projects', {
      method: "POST",
      headers: {
        "Content-Type" : "application/json"
      },
      body: JSON.stringify({
        title: this.title,
        detail: this.detail,
        complete: false 
      })
    })
      .then(() => {
        this.$router.push("/");
      })
      .catch((err) => {
        console.log(err);
    })
  }
},
}
</script>

<style>
form{
  background: white;
  padding: 20px;
  border-radius: 10px;
}
label{
  display: block;
  color: #bbb;
  text-transform: uppercase;
  font-size: 14px;
  font-weight: bold;
  letter-spacing: 1px;
  margin: 20px 0 10px 0;
}
input{
  padding: 10px;
  border: 0;
  border-bottom: 1px solid #ddd;
  width: 100%;
  box-sizing: border-box;
}
textarea{
  border: 1px solid #ddd;
  padding: 10px;
  width: 100%;
  box-sizing: border-box;
  height: 100px;
}
form button{
  display: block;
  margin: 20px auto 0;
  background: #00ce89;
  color: white;
  padding: 10px;
  border: 0;
  border-radius: 6px;
  font-size: 16px;
}
</style>