<template>
    <div>
        <h1>{{ header }}</h1>
        <div class="row">
            <div class="col-sm-6">

                <ul class="list-group">
                    <li @click="selectCountry(country)"
                        class="list-group-item"
                        v-for="country in data.countries"
                        :key="country.id">
                <span :id="country.id"
                      :title="country.details">
                    {{ country.id }} - {{country.name}}
                </span>
                    </li>
                </ul>
                <button @click="decrement()"  class="btn btn-success">vorige</button>
                <button @click="increment()"  class="btn btn-success">volgende</button>
                <button @click="toggleDetails()"  class="btn btn-success">details</button>
                <br>
                {{text}}
            </div>
            <div class="col-sm-6" v-if="details">
                <h2>{{selectedCountry.name}}</h2>
                <ul class="list-group">
                    <li class="list-group-item">{{ selectedCountry.id}}</li>
                    <li class="list-group-item">{{ selectedCountry.name}}</li>
                    <li class="list-group-item">{{ selectedCountry.capital}}</li>
                    <li class="list-group-item">{{ selectedCountry.details}}</li>
                    <li class="list-group-item"><img class="img-fluid" :src="getImgUrl(selectedCountry.img)" :alt="selectedCountry.img"></li>
                    <li class="list-group-item" v-if="isOnSale">
                        <span class="badge badge-danger badge-pill">On Sale!</span>
                    </li>
                    <li class="list-group-item" v-if="isExpensive">
                        <span class="badge badge-danger badge-pill">Expensive!</span>
                    </li>

                </ul>
            </div>
        </div>
        <hr>

    </div>


</template>

<script>
    import countryData from '../data/countryData';
    import mixins from '../mixins/mixins';

    export default {
        name: "Countries",
        mixins:[mixins],
        data() {
            return {
                data:countryData,
                header: "Countries",
                selectedCountryIndex: 0,
                details:true,
                text:'ik win',
            }
        },
        methods: {
            selectCountry(country) {
                this.selectedCountryIndex = this.data.countries.indexOf(country);
            },
            getImgUrl(img) {
                return require('../assets/countries/'+img);
            },
            increment() {
                if (this.selectedCountryIndex < this.data.countries.length-1 ) {
                    this.selectedCountryIndex++;
                }
            },
            decrement(){
                if (this.selectedCountryIndex>0)
                    this.selectedCountryIndex--;
            },
            toggleDetails() {
                if (this.details === true)
                    this.details = false;
                else
                    this.details = true;
            }
        },
        computed: {
            selectedCountry() {
                console.log('selectedCountry aangeroepen');
                return {
                    // longhand notation: annotate every property
                    // id: this.data.countries[this.selectedCountryIndex].id,
                    // name: this.data.countries[this.selectedCountryIndex].name,
                    // capital: this.data.countries[this.selectedCountryIndex].capital,
                    // cost: this.data.countries[this.selectedCountryIndex].cost,
                    // details: this.data.countries[this.selectedCountryIndex].details,
                    // img: this.data.countries[this.selectedCountryIndex].img

                    // shorthand notation: use the spread operator
                    // (=more elegant & scalable)

                    ...this.data.countries[this.selectedCountryIndex]
                }
            },
            isOnSale() {
                return this.data.countries[this.selectedCountryIndex].cost < 1000;
            },
            isExpensive(){
                return this.data.countries[this.selectedCountryIndex].cost > 4000;
            }
        },
        created(){
            console.log('start');
            //window.alert('start');
            this.text="Tekst uit de lifecycle hook created";
        }
    }
</script>

<style scoped>

</style>