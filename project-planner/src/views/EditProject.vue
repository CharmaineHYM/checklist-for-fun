<template>
  <form @submit.prevent="UpdateProject">
      <label>Title:</label>
      <input type="text" required v-model="title">
       <label>Details:</label>
       <textarea required v-model="detail"></textarea>
       <button>Update Project</button>
  </form>
</template>

<script>
export default {
    props: ['id'],
    data(){
        return{
            title: '',
            detail: '',
            uri: 'https://my-json-server.typicode.com/CharmaineHYM/check-list-data/projects/' + this.id
        }
    },
    mounted(){
        fetch(this.uri)
        .then(res => res.json())
        .then(data => {
           this.title = data.title
           this.detail = data.detail 
        })
    },
    methods:{
        UpdateProject(){
            fetch(this.uri, { 
                method: 'PATCH',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({ 
                    title: this.title, 
                    detail: this.detail})
             })
            .then(() => this.$router.push('/'))
            .catch(err => console.log(err.message))
        }
    }
}
</script>

<style>

</style>