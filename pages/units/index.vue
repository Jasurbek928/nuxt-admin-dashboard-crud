<template>
  <List :settings="settings" />
</template>
<script>
export default {
  data(){
     return{
      items:[],
      settings:{
        pageTitle:'Birliklar',
        routes:{
          create:'/units/create',
          update:'/units/update'
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

        ],
        apis:{
          list:'/wms/units'
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
