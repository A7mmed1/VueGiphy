<template >
    <div>
        <div class="container">
            <div class="gif">
                    <h5>Gif</h5>
                <div class="dropDown">
                    <div >
                        Chosse Gif
                        <form class="form-group mt-5 p-4" @submit.prevent="doSearch">
                            <input v-model="query" type="text" placeholder="Gif">
                            <button  type="submit"  class="btn btn-primary">Search</button>

                        </form>
                    </div>

                    <ul class="">
                        <li   @click="chosseOne(index)" v-for="(result, index) in results">
                        <img   :src="result.images.fixed_height.url">
                        </li>
                    </ul>
                        <hr>
                    </div>
                        <div class="one">
                            <h1>Selected</h1>
                            <img :src="this.selected" alt="">
                        </div>

            </div>

        </div>

    </div>

</template>

<script>
import  Result from './Result.vue'
import axios from 'axios'
export default {
    components:{Result},
    data(){
        return {
            apikey: 'dgzg8JSglLqdorSpm6NpUBLLqQPqtbJb',
            query: '',
            results :[],

            selected: null
        }
    },

    methods : {
        doSearch() {
            axios.get('https://api.giphy.com/v1/gifs/trending?api_key=' + this.apikey + '&q=' + this.query)
            .then ((response) => {
                this.results = response.data.data ;
            })
        },
        chosseOne(index){

            this.selected = this.results[index].images.fixed_height.url


        }
    }
}
</script>

<style lang="scss" >
*{
    background-color: #eeeeee;
}
ul{
    list-style:  none;
}
li{
    float: left;
    padding: 10px;
}
img{
    width: 100px;
    float: right;
    display:inline-block;
}
.gif{
    position: relative;
    width: 50%;
    padding: 0;
    margin-top: 10px;

}
.dropDown{
    display: none;
    position: absolute;
    top: 42px;
    left: 0;
    width: 220px;
    padding:10px;
    box-shadow: 0 1px 1px rgba(0,0,0,.5);



}
.one{
    float:right;
    img{
        width: 250px;
    }
}
.gif:hover  .dropDown{
    display: block;;
}



</style>
