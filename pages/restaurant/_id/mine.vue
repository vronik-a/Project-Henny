<template>
  <div>
    <h1>Restaurants</h1>
    <div class="restaurant">
      <div v-for="meal in meals.data" :key="meal.id" class="rest">
          <b-card
            :title="meal.name"
            img-alt="Image"
            :img-src="meal.image"
            img-top
            tag="article"
            style="max-width: 20rem;"
            lass="mb-2"
            img-fluid
          >
            <b-card-text>
              {{ meal.description }}
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
        query getMeals($id: ID) {
            meal(id: $id) {
              id
              image
              name
              price
              description
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
.restaurant{
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  align-items: center;
  overflow: hidden;
  flex-wrap: wrap;
  margin: 30px;
}
h1{
  margin: 20px;
}
.rest{
  width: 20%;
}
.rest a {
  color: black;
}
@media (max-width: 576px) {
  h1{
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 0;
  }
  .rest{
    width: 50%;
  }
}
@media (max-width: 768px) {
  h1{
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 0;
  }
  .rest{
    width: 40%;
  }
}
@media (min-width: 769px) and (max-width:1024px) {
  h1{
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 0;
  }
  .rest{
    width: 30%;
  }
}
</style>
