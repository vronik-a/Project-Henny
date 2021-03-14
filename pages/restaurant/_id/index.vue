<template>
  <div>
    <div v-if="!$apollo.queries.restaurant.loading">
      <div class="shop">
        <b-card
          :title="restaurant.name"
          img-src="restaurant.meals[ID].image"
          img-alt="Image"
          img-top
          tag="article"
          style="max-width: 20rem;"
          class="mb-2"
        >
          <b-card-text>
            <span> {{ restaurant.meals[ID].name }} </span>
            <br>
            <span id="price"> {{ restaurant.meals[ID].price }} GH</span>
            <br>
            <span> {{ restaurant.meals[ID].description }} </span>
          </b-card-text>
        </b-card>
      </div>
    </div>
  </div>
</template>

<script>
import gql from 'graphql-tag'
export default {
  apollo: {
    restaurant: {
      prefetch: true,
      query: gql`
        query getRestaurant($id: ID) {
          restaurant(id: $id) {
            id
            name
            slug

            meals($id: ID){
              id
              image
              name
              price
              description
            }
          }
        }
      `,
      variables () {
        return {
          id: this.$route.params.id
        }
      }
    }
  }
}
</script>

<style>
.shop {
  margin-top: 80px;
}
</style>
