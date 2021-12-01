<template>
  <List :settings="settings" />
</template>
<script>
export default {

  data(){
    return{
      items:[],
      settings:{
        pageTitle:'Mahsulotlar',
        routes:{
          create: '/products/create',
          update: '/products/update/'
        },
        apis:{
          list: '/wms/products'
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
          },
          {
            title: 'Description',
            component: 'ListText',
            property: 'description'
          },
          {
            title: 'Category',
            component: 'ListCategory',
            property: 'category'
          }
      ]
      },
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
