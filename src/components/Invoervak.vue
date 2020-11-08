<template>
    <div class="row">
        <div class="col">
            <hr>
            <h2>Countries </h2>
            <input type="text" v-model="newCountry" @keyup.enter="addCountry(newCountry)"
            class="form-control-lg" placeholder="New Country..."/>
            <button @click="addCountry()"
                    class="btn btn-info">Add Country</button>

            <ul class="list-group">
                <li v-for="(country, index) in newCountries"
                    :key="index"
                    class="list-group-item">
                    {{ country }}
                    <button class="btn btn-danger" @click="deleteCountry(index)">Delete</button>
                </li>
            </ul>

        </div>
    </div>
</template>

<script>
    export default {
        name: "Invoervak",
        data() {
            return {
                newCountry:'',
                newCountries: []
            }
        },
        methods:{
            addCountry() {
                this.newCountries.push(this.newCountry);
                this.newCountry='';
            },
            deleteCountry(index){
                //window.alert(index);
                this.newCountries.splice(index,1);
            }
        }
    }
</script>

<style scoped>

</style>