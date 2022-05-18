<template>
  <section class="min-h-screen w-full flex items-center justify-center bg-gradient-to-tr from-pink-300 to-purple-300">
    <div v-if="$apollo.queries.characters.loading">
      <h2>Loading...</h2>
    </div>
    <ul v-else class="bg-white rounded-lg shadow-md p-4 grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4 my-10">
      <li @click="$router.push(`/member/${item.id}`)" v-for="item in characters.results" :key="item.id" class="flex gap-6 bg-[#f1f1f1] p-4 rounded-lg shadow-md cursor-pointer hover:shadow-inner">
        <img :src="item.image" :alt="item.name" class="w-14 h-14 rounded-full">
        <div class="grid grid-cols-12 w-full">
          <div class="col-span-3">Name</div>
          <div class="col-span-9">{{ item.name }}</div>
          <div class="col-span-3">Gender</div>
          <div class="col-span-9">{{ item.gender }}</div>
          <div class="col-span-3">Location</div>
          <div class="col-span-9">{{ item.location.name }}</div>
        </div>
      </li>
    </ul>
  </section>
</template>

<script>
import gql from 'graphql-tag'
export default {
  name: 'IndexPage',
  apollo: {
    characters: gql`
      query getCharacters {
        characters {
          results {
            id
            name
            gender
            image
            location {
              name
              type
            }
          }
        }
      }
    `
  }
}
</script>
