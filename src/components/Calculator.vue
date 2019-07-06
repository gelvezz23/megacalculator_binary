<template>
    <div>
        <div class="form">
            <input v-model="number1" type="text">
            <input v-model="number2" type="text">
            <div class="separator"></div>
            <input v-model="result" type="text" readonly="readonly">
            <div class="action">
                <button class="btn" @click="calculate('sumadecimal')">+ <span class="exponent">2</span></button>
                <button class="btn" @click="calculate('sumabinaria')">+ <span class="exponent">10</span></button>
                <button class="btn" @click="calculate('restadecimal')">-<span class="exponent">2</span></button>
                <button class="btn" @click="calculate('restabinaria')">-<span class="exponent">10</span></button>
            </div>
            <div class="history">
                <button @click="getHistory" class="btn">Historial</button>
            </div>
        </div>

        <transition name="fade">
            <div class="error" v-show="history.show">
                <div class="modal" v-bind:class="[history.data.length > 0 ? 'start' : 'center']">
                    <div class="close">
                        <div class="btn" @click="history.show = false">X</div>
                    </div>

                    <div class="message">
                        <template v-if="history.data.length > 0">
                            <ul class="header">
                                <li>Número 1</li>
                                <li>Número 2</li>
                                <li>Operación</li>
                            </ul>
                            <ul class="content-history">
                                <li v-for="(op,index) in history.data" :key="index" class="item-history">
                                    <span>{{op.numero1}}</span>
                                    <span>{{op.numero2}}</span>
                                    <span>{{op.operacion}}</span>
                                </li>
                            </ul>
                        </template>
                        <template v-else>
                            <span class="message-error">
                                {{history.message}}
                            </span>
                        </template>
                    </div>
                </div>
            </div>
        </transition>
    </div>
</template>

<script>
    export default {
        name: 'Calculator',

        data: () => ({
            HOST: '0.0.0.0:8000', // ** Modified HOST
            number1: 0,
            number2: 0,
            result: 0,
            history: {
                show: false,
                message: null,
                data: []
            }
        }),

        methods: {
            calculate(type) {
                // ** connection at the API
                fetch(this.HOST + '/' + type, {
                    method: 'post',
                    data: JSON.stringify({'numero1': this.number1, 'numero2': this.number2}),
                    headers: {
                        'Content-Type': 'application/json',
                    }
                }).then(response => {
                    response.json().then(response => {
                        if (response.status === 200) {
                            this.result = response.resultado;
                        } else {
                            this.result = response.mensaje;
                        }
                    })
                })
            },

            getHistory() {
                this.history.show = true;

                // ** connection at the API
                fetch(this.HOST + '/historial', {
                    method: 'get',
                }).then(response => {
                    response.json().then(response => {
                        if (response.status === 200) {
                            this.history = response.resultado;
                        } else {
                            this.history.message = response.mensaje;
                        }
                    })
                });
            }
        }

    }
</script>

<style scoped lang="scss">
    @import "../style/calculator";


    .fade-enter-active, .fade-leave-active {
        transition: opacity .5s;
    }

    .fade-enter, .fade-leave-to {
        opacity: 0;
    }
</style>
