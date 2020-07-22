<template>
    <v-container  grid-list-md>
        <v-layout  xs7 md8 row>
            <v-col cols="12" md="8">
                <v-flex  xs12 sm10 md8 offset-sm1 offset-md-2>
                    <v-container>
                        <v-layout row>
                            <v-flex xs7 md8>
                                <v-text-field label="qiriqish" v-model="searchCart"></v-text-field>
                            </v-flex>
                            <v-flex xs5 md4>
                                <v-select label="positsiya" :items="poss" v-model="pos" multiple ></v-select>
                            </v-flex>
                        </v-layout>
                    </v-container>
                </v-flex>
                <v-flex v-for="player in filteredPlayers" :key="player.id" xs12 sm10 md8 offset-sm1 offset-md-2>
                    <v-card color="info" class="white--text">
                        <v-container fluid>
                            <v-layout row>
                                <v-flex xs4 md3>
    <!--                                <img class="mx-2" :src="player.img" height="100px">-->
                                    <div>
                                    <v-img :elevation="15"  class="mx-2" :src="player.img" height="100px">
                                    </v-img>
                                        <div class="text-xs-center">
                                            <img  style="padding: 5px 0 0 5px; height: 35px"  src="img/youtube.png" >
                                        </div>
                                        <div class="hidden-md-and-up">
                                            <v-btn :elevation="10" style="background: red ;color: white;" flat>ko'rish</v-btn>
                                        </div>
                                    </div>
                                </v-flex>
                                <v-flex xs8 md9>
                                    <v-card-title class="pa-0">
                                        <div>
                                            <div>{{player.name}}</div>
                                            <div  style="font-size: 15px; font-family: italic">Yoshi: {{player.age}} Raqami: {{player.number}}</div>
                                            <div style="font-size: 15px; font-family: Icons">Positsiyasi: {{getPositsion(player.pos)}}</div>
                                            <v-divider class="white"></v-divider>
                                        </div>
                                    </v-card-title>
                                    <v-card-actions>
                                        <v-rating readonly dense half-increments color="red" v-model="player.rating"></v-rating>
                                        <div style="font-size: 15px" class="ml-1">
                                            <span>{{player.rating}}</span>
                                            <span>({{player.ratingCOunt}})</span>
                                        </div>
                                        <v-spacer></v-spacer>
                                        <div class="hidden-sm-and-down">
                                            <v-btn :elevation="15"  class="red" style="color: white" flat>ko'rish</v-btn>
                                        </div>
                                    </v-card-actions>

                                </v-flex>
                            </v-layout>
                        </v-container>
                    </v-card>
                </v-flex>
            </v-col>
                <v-col cols="6" md="4">

                    <v-spacer></v-spacer>
                    <v-btn class="mx-2" fab dark color="indigo">
                        <v-icon dark>mdi-plus</v-icon>
                    </v-btn>
                </v-col>
        </v-layout>


    </v-container>
</template>

<script>

    export default {
        methods:{
            getPositsion(pos){
                return pos.join('/')
            }
        },
        computed:{
            filteredPlayers(){
                let players = this.players
                if(this.searchCart)
                    players = players.filter(p =>
                        p.search.toLowerCase().indexOf(this.searchCart.toLowerCase()) >=0)
                    // &&  p.number.toLowerCase().indexOf(this.searchCart.toLowerCase()) >=0)
                if (this.pos.lenght)
                    players = players.filter(b => this.pos.filter(val=>b.pos.indexOf(val)!==-1).length>0)

                return players;
            }
        },
        data() {
            return {
                searchCart: null,
                pos: [],
                poss: ['ss','cf','rfs','amf','cmf'],

                players:[
                    {
                        id: 1,
                        name: 'Muhammed Salah',
                        age:28,
                        imageId: 1,
                        number:11,
                        rating: 4,
                        ratingCOunt: 100,
                        pos:['ss', 'cf', 'rfs'],
                        youtube_play_id: 'kjhgkhgk',
                        img: 'img/salah.jpg',
                        search: 'Muhammed Salah 28 11 мухаммед салах'
                    },
                    {
                        id: 2,
                        name: 'Sadio Mane',
                        age:28,
                        imageId: 2,
                        number: 10,
                        rating: 4.5,
                        ratingCOunt: 85,
                        pos:['ss', 'lfs'],
                        youtube_play_id: 'kkjhjhgkhgk',
                        img: 'img/mane.jpg',
                        search:'mane 28 10'
                    },
                    {
                        id: 3,
                        name: 'Roberto Firminho',
                        age: 28,
                        imageId: 3,
                        number: 9,
                        rating: 4,
                        ratingCOunt: 80,
                        pos:['ss', 'cf'],
                        youtube_play_id: 'kjhoiouihgkhgk',
                        img: 'img/firminyo.jpg',
                        search: 'roberto 28 9'
                    },
                    {
                        id: 4,
                        name: 'Jordan Henderson',
                        age: 30,
                        imageId: 4,
                        number: 14,
                        rating: 3.5,
                        ratingCOunt: 75,
                        pos:['amf', 'cmf'],
                        youtube_play_id: 'kjhgkigoiughgk',
                        img: 'img/hendo.jpg',
                        search: 'jordan 30 14'
                    }
                ]
            }
        }

    }
</script>

<style scoped>

</style>