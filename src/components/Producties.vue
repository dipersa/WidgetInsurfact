<template>
    <div style="margin-left: 11px;margin-right: 11px" class="card_insurfact">
        <div class="card_insurfact-title center_insurfact" style="background-color: rgb(24, 105, 149); padding: 1px">
            <h5 class="white-text" style="font-weight: bold !important; text-align: left !important; margin-left: 20px !important" >Select a product</h5>
        </div>
        <div class="card_insurfact-content center_insurfact">
            <div v-if="loading" class="preloader-wrapper_insurfact big_insurfact active_insurfact">
                <div class="spinner-layer_insurfact spinner-blue-only_insurfact">
                    <div class="circle-clipper_insurfact left_insurfact">
                        <div class="circle_insurfact"></div>
                    </div>
                    <div class="gap-patch_insurfact">
                        <div class="circle_insurfact"></div>
                    </div>
                    <div class="circle-clipper_insurfact right_insurfact">
                        <div class="circle_insurfact"></div>
                    </div>
                </div>
            </div>
            <h4 class="center_insurfact red-text" v-if="errored==true">{{err}}An unexpected error occurred. Try again later</h4>
            <div v-if='companies!=null && errored==false'>
                <div class="row_insurfact">
                    <div v-for="i in n" :key="i">
                        <tarjeta :loans="loans" :amortization="amortization" :quote="quote" :company="companies[i-1]" :key="companies[i-1].company_desc_en"></tarjeta>
                    </div>
                </div>
                <a v-on:click="expandList" class="waves-effect_insurfact waves-teal_insurfact btn-flat_insurfact" style="color: rgb(24, 105, 149); font-weight: bold">{{textobutton}}</a>
            </div>
            <div v-if="is204">
                <h4 class="center_insurfact">There is no information to show.</h4>
            </div>
        </div>
    </div>
</template>

<script>
    import Tarjeta from "./Tarjeta";

    export default {
        name: "Producties",
        components: {Tarjeta},
        data: () => ({
            n: 8,
            textobutton: 'Expand list'
        }),
        props: ['companies', 'errored', 'is204', 'loading','quote','amortization','loans'],
        methods: {
            expandList: function () {
                if (this.n == 8) {
                    this.textobutton = 'Collapse list'
                    this.n = this.companies.length
                } else {
                    this.textobutton = 'Expand list'
                    this.n = 8
                }
            }
        }
    }
</script>
