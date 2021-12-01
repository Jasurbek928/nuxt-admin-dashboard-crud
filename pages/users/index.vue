<template>
  <List :settings="settings" />
</template>

<script>
export default {
  data() {
    return {
      items: [],
      settings:{
        pageTitle:'Foydalanuvchilar',
        routes:{
          create: '/users/create',
          update: '/users/update/'
        },
        apis:{
          list: '/user/users'
        },
        headers:[
           {
            title: 'Name',
            component: 'ListProfile',
            property: 'name'
          },
          {
            title: 'Title',
            component: 'ListAddress',
            property: 'title'
          },
          {
            title: 'Status',
            component: 'ListStatus',
            property: 'status'
          },
          {
            title: 'Role',
            component: 'ListText',
            property: 'role'
          }

        ]
      }
    }
  },
  mounted() {
    this.loadItems()
  },
  methods: {
    loadItems() {
      this.$axios
        .$get(this.settings.apis.list)
        .then((res) => (this.items = res.items.data))
    }
  }
}
</script>

<style>
</style>
