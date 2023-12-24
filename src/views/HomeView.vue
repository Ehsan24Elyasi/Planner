<template>
  <div class="home">
    <updatefilter @filterchange="current = $event" :current="current"  />
    <div v-if="projects.length">
      <div v-for="project in filteredprogect" :key="project.id">
        <singleproject @delete="hadledelete" @copmlate="handelcopmlate" :project="project" />
      </div>
  </div>
</div>
</template>

<script>
import singleproject from '../components/singleproject.vue'
import updatefilter from '../components/FilterNav.vue'

export default {
  name: 'HomeView',
  components: {singleproject,updatefilter},
  data() {
    return{
      projects:[],
      current:'all'
    }
  },

  mounted()
  {
    fetch('http://localhost:3000/projects')
      .then(res => res.json())
      .then(data => this.projects = data)
  },

  methods:
  {
    hadledelete(id){
      this.projects = this.projects.filter(item => {
        return item.id !== id
      })
    },
    handelcopmlate(id)
    {
        let p = this.projects.find(item => {
          return item.id === id
        })
          p.copmlate = !p.copmlate
    }
  },
  computed:
  {
      filteredprogect()
    {
      if (this.current == 'completed')
      {
        return this.projects.filter(item => item.copmlate)
      }
      else if (this.current == 'ongoing')
      {
        return this.projects.filter(item => !item.copmlate)
      }
      else
      {
        return this.projects
      }
    }
  }
}
</script>
