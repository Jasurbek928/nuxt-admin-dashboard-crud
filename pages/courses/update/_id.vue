<template>
  <div class="min-h-full">
    <Navigation />

    <header class="bg-white shadow">
      <div class="max-w-7xl mx-auto py-6 px-4 sm:px-6 lg:px-8">
        <h1
          class="text-3xl font-bold text-gray-900"
        >Kursni tahrirlash: {{ $route.params.id }}</h1>

      </div>
    </header>
    <main>
      <div class="max-w-7xl mx-auto py-6 sm:px-6 lg:px-8">
        <!-- Replace with your content -->
        <div class="px-4 py-6 sm:px-0">
          <!-- This example requires Tailwind CSS v2.0+ -->
          <div class="flex flex-col">
            <div class="-my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
              <div class="py-2 align-middle inline-block min-w-full sm:px-6 lg:px-8">
                <div class="mt-5 md:mt-0 md:col-span-2">
                  <div class="shadow overflow-hidden sm:rounded-md">
                    <div class="px-4 py-5 bg-white sm:p-6">
                      <div class="grid grid-cols-6 gap-6">
                        <FormInput v-model="course.name" label="Name" />
                        <FormInput v-model="course.price" label="Price" />
                      </div>
                    </div>
                    <div class="px-4 py-3 bg-gray-50 text-right sm:px-6">
                      <button
                        class="inline-flex justify-center py-2 px-4 border border-transparent shadow-sm text-sm font-medium rounded-md text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500"
                        @click="updateCourseData"
                      >Save</button>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
        <!-- /End replace -->
      </div>
    </main>
  </div>
</template>

<script>
export default {
  data() {
    return {
      course: {
        id: null,
        name: null,
        price: null,
      },
    }
  },
  mounted() {
    this.getCourseData()

  },
  methods: {
    getCourseData() {
      this.$axios.get('/lms/courses/' + this.$route.params.id).then((res) => {
        this.course = res.data.item
      })
    },
    updateCourseData() {
      const formData = new FormData()
      formData.append('_method', 'PUT')
      for (const key in this.course) {
        if (this.course[key] != null) {
          if (typeof this.course[key] === 'object' && key !== 'image') {
            for (const k in this.course[key]) {
              formData.append(`${key}[${k}]`, this.course[key][k])
            }
          } else {
            formData.append(key, this.course[key])
          }
        }
      }
      this.$axios
        .post('/lms/courses/' + this.$route.params.id, formData)
        .then((res) => {
          this.$router.push('/courses')
        })
    },
  }
}
</script>

<style>
</style>
