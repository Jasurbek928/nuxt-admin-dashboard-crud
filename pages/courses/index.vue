<template>
  <List :settings="settings" />
</template>
<script>
export default {
  data(){
    return{
      items:[],
      settings:{
        pageTitle:'Kurslar',
        routes:{
          create:'/courses/create',
          update:'/courses/update'
        },
        headers:[
          {
            title: 'ID',
            component: 'ListText',
            property: 'id'
          },
          {
            title: 'Name',
            component: 'ListText',
            property: 'name'
          },
          {
            title: 'Price',
            component: 'ListText',
            property: 'price'
          }
        ],
        apis:{
          list:'/lms/courses'
        }
      }
    }
  },
  mounted(){
    this.loadItems()
  },
  methods:{
    loadItems(){
      this.$axios.$get(this.settings.apis.list)
      .then((res)=>
        (this.items=res.items.data))
    }
  }
}
</script>

<style>

</style>
