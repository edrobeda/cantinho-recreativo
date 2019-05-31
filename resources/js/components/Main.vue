<template>
    <div class="container">
        <div class="row">
            <div class="col-md-12">
            {{ saudacao }}, {{ name }}<br>{{ test }}
            </div>
        </div>
    </div>
</template>

<script>
    var moment = require('moment');

    const helpers = require('../helper/helpers')
    export default {
        data(){
            return {
                saudacao: "",
                name: "",
                test: ""
            }
        },
        mounted() {
            console.log('Component mounted.')
        },
        created(){
            this.executeThis(),
            this.getName(),
            this.getSaudacao()

        },
        methods: {
            // moment: function () {
            //     return moment();
            // },
            executeThis(){
                fetch('https://api.preprod.bsfonline.com.br/emails/run-queue')
                .then((res)=> res.json())
                .then(res => {
                    this.test = res
                })
                .catch(err => console.log(err))
            },
            getName(){
                this.name = 'Edson'
            },
            getSaudacao(){
                let hourOfTheDay = this.getDate().format('h');
                this.saudacao = ( hourOfTheDay > 2  || hourOfTheDay <= 12 ) ? 'Bom Dia'   :
                                ( hourOfTheDay > 12 || hourOfTheDay <= 18 ) ? 'Boa tarde' : 'Boa Noite'
            },
            getDate(){
                return moment()
            }

        }
    }
</script>
