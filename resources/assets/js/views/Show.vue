/**
 * Template for the Show Drink page.
 * If I was to build the API for that,
 * I wouldn't use a separate variable name for each 15 slots of ingredients.
 * They should be rather stored in the object, so I could easily loop through table.
 */
<template>
    <div class="row">
        <div class="col s12 m6 left">
            <div class="card">
                <div class="card-content">
                    <h4>{{drink.strDrink}}</h4>
                    <h5 class="grey-text text-darken-3">Base: {{drink.strAlcoholic}}</h5>
                    <h6 class="grey-text text-darken-3">Category: {{drink.strCategory}}</h6>
                    <h6 class="grey-text text-darken-3">Glass: {{drink.strGlass}}</h6>
                    <br>
                    <p>{{drink.strInstructions}}</p>

                </div>
                <div class="card-action">
                    <a v-if="this.favouritesID.includes(drink.idDrink)" @click="removeFavourite(drink)" class="cursor-pointer">Remove Favourite</a>
                    <a v-else="this.favouritesID.includes(drink.idDrink)" @click="addFavourite(drink)" class="cursor-pointer">Add Favourite</a>
                </div>
            </div>
        </div>
        <div class="col s12 m6 right">
            <div class="card-panel hoverable no-padding">
                <p class="center-align">
                    <img class=" materialboxed responsive-img" :src="drink.strDrinkThumb">
                </p>
            </div>
        </div>
        <div class="col s12 m6 left">
            <div class="card-panel">
                <table class="highlight">
                    <thead>
                        <tr>
                            <th>Ingredient</th>
                            <th>Amount</th>
                        </tr>
                    </thead>

                    <tbody>
                        <tr v-if="drink.strIngredient1">
                            <td>{{drink.strIngredient1}}</td>
                            <td>{{drink.strMeasure1}}</td>
                        </tr>
                        <tr v-if="drink.strIngredient2">
                            <td>{{drink.strIngredient2}}</td>
                            <td>{{drink.strMeasure2}}</td>
                        </tr>
                        <tr v-if="drink.strIngredient3">
                            <td>{{drink.strIngredient3}}</td>
                            <td>{{drink.strMeasure3}}</td>
                        </tr>
                        <tr v-if="drink.strIngredient4">
                            <td>{{drink.strIngredient4}}</td>
                            <td>{{drink.strMeasure4}}</td>
                        </tr>
                        <tr v-if="drink.strIngredient5">
                            <td>{{drink.strIngredient5}}</td>
                            <td>{{drink.strMeasure5}}</td>
                        </tr>
                        <tr v-if="drink.strIngredient6">
                            <td>{{drink.strIngredient6}}</td>
                            <td>{{drink.strMeasure6}}</td>
                        </tr>
                        <tr v-if="drink.strIngredient7">
                            <td>{{drink.strIngredient7}}</td>
                            <td>{{drink.strMeasure7}}</td>
                        </tr>
                        <tr v-if="drink.strIngredient8">
                            <td>{{drink.strIngredient8}}</td>
                            <td>{{drink.strMeasure8}}</td>
                        </tr>
                        <tr v-if="drink.strIngredient9">
                            <td>{{drink.strIngredient9}}</td>
                            <td>{{drink.strMeasure9}}</td>
                        </tr>
                        <tr v-if="drink.strIngredient10">
                            <td>{{drink.strIngredient10}}</td>
                            <td>{{drink.strMeasure10}}</td>
                        </tr>
                        <tr v-if="drink.strIngredient11">
                            <td>{{drink.strIngredient11}}</td>
                            <td>{{drink.strMeasure11}}</td>
                        </tr>
                        <tr v-if="drink.strIngredient12">
                            <td>{{drink.strIngredient12}}</td>
                            <td>{{drink.strMeasure12}}</td>
                        </tr>
                        <tr v-if="drink.strIngredient13">
                            <td>{{drink.strIngredient13}}</td>
                            <td>{{drink.strMeasure13}}</td>
                        </tr>
                        <tr v-if="drink.strIngredient14">
                            <td>{{drink.strIngredient14}}</td>
                            <td>{{drink.strMeasure14}}</td>
                        </tr>
                        <tr v-if="drink.strIngredient15">
                            <td>{{drink.strIngredient15}}</td>
                            <td>{{drink.strMeasure15}}</td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
    </div>
</template>

<script>
import FetchSingle from '../models/FetchSingle';

export default {
    data() {
        return {
            drink: {},
        }
    },
    methods: {
        addFavourite (object) {
            // add to favourite drinks
            store.commit('addFavourite', object);
        },
        removeFavourite (object) {
            // remove from favourite drinks
            store.commit('removeFavourite', object);
        },
        /**
         * Get the data of a drink based on the url ID
         */
        updateDrink () {
            if(this.$route.params.id)
                FetchSingle.id(this.$route.params.id)
                    .then(response => this.drink = response.data.drinks[0]);
            // Initialize the image zoom in effect
            $(document).ready(function(){
                $('.materialboxed').materialbox();
            });
        }
    },
    created () {
        // Get the drink data after initialized
        this.updateDrink();
    },
    watch: {
        /**
         * Reload the drink data if the url changes
         */
        '$route' (to, from) {
            this.updateDrink();
        },
    },
    computed: {
        /**
         * Binds dynamic favouritesID and favouritesObjects values taken from Vuex storage.
         */
        favouritesID () {
            return store.state.favouritesID;
        },
        favouritesObjects () {
            return store.state.favouritesObjects;
        },
    }
}
</script>
