<template>
    <div >
        <select v-model="valuta">
            <option disabled value="">Please select one</option>
            <option>EUR</option>
            <option>USD</option>
            <option>GBP</option>
        </select>


        <h1>{{ header }}</h1>
        <ul class="list-group">
            <li class="list-group-item"
                v-for="country in data.countries" :key="country.id">
                <span :id="country.id"
                      :title="country.details">
                    {{ country.id }} - {{country.name | uppercase }} - {{country.cost |currency(valuta)}}
                </span>
            </li>
        </ul>
    </div>
</template>

<script>
    import data from '../data/countryData';
    export default {
        name: "Filtering",
        data() {
            return {
                data,
                valuta:'EUR',
                header: 'List of destinations',

            }
        },
        // creating a local filter, called 'uppercase'. This is used in the UI
        filters:{
            uppercase(value){
                if(!value){
                    return;
                }
                return value.toUpperCase();
            },
            currency(value,currency) {
               if (!value) return;
               return new Intl.NumberFormat('nl-NL',{
                   style:"currency",
                   currency:currency
               }).format(value);
            }
        }
    }
</script>

<style scoped>

</style>