<template>
  <div class="project" :class="{copmlate: project.copmlate}">
    <div class="action">
        <h3 @click="showdetails()">{{ project.title }}</h3>
        <div class="icons">
            <i class="bi bi-check-circle" @click="changecopmlate()" ></i>
            <i class="bi bi-x-circle" @click="Deleteproject()"></i>
            <router-link :to="{name: 'EditProject' , params:{id:project.id}}">
            <i class="bi bi-pencil" ></i>
            </router-link>
        </div>
    </div>
    <div v-if="detailscondition" class="details">
        <p>{{ project.details }}</p>
    </div>
  </div>
</template>

<script>
export default {
props: ['project'],
data()
{
return{
    detailscondition:false,
    uri: 'http://localhost:3000/projects/' + this.project.id
}
},
methods: {
    showdetails()
    {
        this.detailscondition = !this.detailscondition
    },

    Deleteproject()
    {
        fetch(this.uri , {method: 'DELETE'})
            .then(() => this.$emit('delete' , this.project.id))
            .catch(err => console.log(err.massage))
    },
    changecopmlate()
    {
        fetch(this.uri , {
            method: 'PATCH',
            headers:{'Content-Type': 'application/json'},
            body: JSON.stringify({copmlate : !this.project.copmlate})
        })
            .then(() => this.$emit('copmlate' , this.project.id))

    }
}
}
</script>

<style>
.project{
margin: 20px auto;
background: white;
padding: 10px 20px;
border-radius: 4px;
box-shadow: 1px 2px 3px rgba(0, 0, 0, 0.5);
border-left: 10px solid #e90074;
}
h3{
    cursor: pointer;
}
.action
{
    display: flex;
    justify-content: space-between;
    align-items: center;;
}

.bi
{
font-size: 24px;
margin-left: 10px;
color: #bbb;
cursor: pointer;
}

.bi:hover
{
    color: #777;
}

.project.copmlate
{
    border-left: 10px solid #00ce89;
}
</style>