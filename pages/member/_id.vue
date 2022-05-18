<template>
  <section class="min-h-screen w-full flex items-center justify-center">
    <div v-if="$apollo.queries.character.loading">
      <h2 class="text-4xl font-bold">Loading...</h2>
    </div>
    <div v-else>
      <button @click="$router.push('/')" class="mb-4 px-4 py-2 bg-gradient-to-tr from-pink-300 to-purple-300 text-white rounded-md">to prev page</button>
      <ul class="p-4 bg-[#f1f1f1] rounded-lg shadow-md">
        <li class="flex items-center gap-4">
          <img :src="character.image" :alt="character.name" class="rounded-full">
          <div>
            <p>Name: {{ character.name }}</p>
            <p>Gender: {{ character.gender }}</p>
            <p>Location: {{ character.location.name }}</p>
          </div>
        </li>
      </ul>
    </div>
  </section>
</template>

<script>
import gql from 'graphql-tag'
export default {
  apollo: {
    character: {
      query: gql`
        query getCharacter($id: ID!) {
          character(id: $id) {
            name
            gender
            image
            location {
              name
            }
          }
        }
      `,
      variables() {
        return {
          id: this.$route.params.id
        }
      }
    }
  }
}
</script>
