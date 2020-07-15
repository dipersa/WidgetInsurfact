<template>
    <div>
        <div class="row_insurfact">
            <Mheader></Mheader>
        </div>
        <br>
        <br>
        <div class="row_insurfact">
            <div class="col_insurfact s12 m12 l8">

                <div id="card_1" class="card_insurfact center_insurfact">
                    <div class="card_insurfact-title center_insurfact"
                         style="background-color: rgb(24, 105, 149); padding: 1px">
                        <h6 class="white-text" style="font-weight: bold !important; text-align: left !important; margin-left: 20px !important">Mortgage Rate Survey</h6>
                    </div>
                    <div class="card_insurfact-content" style="padding-bottom: 0px">
                        <h6 class="left_insurfact" style="color: rgb(24, 105, 149); font-weight: bold">Current province / territory of residence</h6>
                        <div class="row_insurfact">
                            <div class="col_insurfact s12 m8 l8 left-align_insurfact">
                                <select v-model="select_province" @change="onChangeValue"
                                        id="select_province" class="browser-default_insurfact">
                                    <option value="0" disabled selected>Selected Province</option>
                                    <option value="AB" selected>Alberta, AB</option>
                                    <option value="BC" selected>British Columbia, BC</option>
                                    <option value="MB" selected>Manitoba, MB</option>
                                    <option value="NB" selected>New Brunswick, NB</option>
                                    <option value="NL" selected>Newfoundland & Labrador, NL</option>
                                    <option value="NT" selected>Northwest Territories, NT</option>
                                    <option value="NS" selected>Nova Scotia, NS</option>
                                    <option value="NU" selected>Nunavut, NU</option>
                                    <option value="ON" selected>Ontario, ON</option>
                                    <option value="PE" selected>Prince Edward Island, PE</option>
                                    <option value="QC" selected>Quebec, QC</option>
                                    <option value="SK" selected>Saskatchewan, SK</option>
                                    <option value="YT" selected>Yukon, YT</option>
                                </select>
                            </div>
                        </div>
                        <div class="row_insurfact center_insurfact">
                            <div class="col_insurfact s12 m4 l4">
                                <select class="browser-default_insurfact" v-model="select_term_value"
                                        @change="onChangeValue"
                                        id="select_term_value">
                                    <option value="0" disabled>Term value</option>
                                    <option value="0.5" default>6 Month</option>
                                    <option value="1">1 Years</option>
                                    <option value="2">2 Years</option>
                                    <option value="3">3 Years</option>
                                    <option value="4">4 Years</option>
                                    <option value="5">5 Years</option>
                                    <option value="10">10 Years</option>
                                </select>

                                <div class="card_insurfact-panel">
                                    <h5 id="years" style="color:rgb(0, 65, 1); font-weight: bold">
                                        {{select_term_value2}}
                                        Years</h5>
                                </div>
                            </div>
                            <div class="col_insurfact s12 m4 l4">
                                <select class="browser-default_insurfact" v-model="select_open_closed"
                                        @change="onChangeValue"
                                        id="select_open_closed">
                                    <option value="0" disabled>Opened/Closed</option>
                                    <option value="O" selected>Open</option>
                                    <option value="C" selected>Closed</option>
                                </select>

                                <div class="card_insurfact-panel ">
                                    <h5 id="open" style="color:rgb(0, 65, 1);font-weight: bold"
                                        v-if='select_open_closed2=="O"'>Open</h5>
                                    <h5 id="closed" style="color:rgb(0, 65, 1); font-weight: bold"
                                        v-if='select_open_closed2=="C"'>Closed</h5>
                                </div>
                            </div>
                            <div class="col_insurfact s12 m4 l4">
                                <select class="browser-default_insurfact" v-model.lazy="select_rate_type"
                                        @change="onChangeValue"
                                        id="select_rate_type">
                                    <option value="0" disabled>Rate Type</option>
                                    <option value="F" selected>Fixed</option>
                                    <option value="V" selected>Variable</option>
                                </select>
                                <div class="card_insurfact-panel">
                                    <h5 id="fixed" style="font-weight: bold;color: rgb(0, 65, 1)"
                                        v-if='select_rate_type2=="F"'>Fixed</h5>
                                    <h5 id="variable" style="font-weight: bold;color: rgb(0, 65, 1)"
                                        v-if='select_rate_type2=="V"'>Variable</h5>
                                </div>
                            </div>
                            <div class="col_insurfact s12 m6 l6 offset-l3 offset-m3">
                                <br>
                                <br>
                                <div v-if="loading" class="preloader-wrapper_insurfact big_insurfactg active_insurfact">
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
                                <div v-if='companies!=null && errored==false' class="row_insurfact">
                                    <div class="col_insurfact s12 m12 l12 card_insurfact">
                                        <div class="card_insurfact-content">
                                            <span class="card_insurfact-title">{{companies[0].company_desc_en}}</span>
                                            <h4 style="font-weight: bold">{{companies[0].interest_rate_value}} %</h4>
                                        </div>
                                        <div class="card_insurfact-action">
                                            <button class="btn_insurfact btn-small_insurfact"
                                                    style="background-color: rgb(39, 89, 195)">
                                                View Rates
                                            </button>
                                        </div>

                                    </div>
                                </div>
                                <div v-if="is204">
                                    <div class="row_insurfact">
                                        <div class="col_insurfact s12 m10 l10 center_insurfact offset-m4 offset-l1">
                                            <h4 class="center_insurfact">There is no information to show.</h4>
                                        </div>
                                    </div>

                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <div class="col_insurfact s12 m12 l4">
                <div class="card_insurfact center_insurfact" style="height: 280px">
                    <div class="card_insurfact-title" style="background-color:rgb(0, 65, 1);padding: 1px">
                        <h6 class="white-text" style="font-weight: bold;">How much money do you need?</h6>
                    </div>
                    <div class="card_insurfact-content">
                        <div class="card_insurfact-panel" style="background-color: rgb(0, 65, 1)">
                            <div id="msform">
                                <br>
                                <div class="row_insurfact">
                                    <div class="col_insurfact s12 m6 l6 offset-l3 offset-m3">
                                        <input class="insur_input" type="number" v-model="loans" placeholder="Prêts"/>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
                <div id="card_2" class="card_insurfact center_insurfact" style="background-color: rgb(24, 105, 149)">
                    <div class="card_insurfact-content">
                        <h4 class="card_insurfact-title white-text">Your quote</h4>
                        <div v-if="minrate>0">

                            <h3 class="white-text truncate_insurfact">$ {{getQuote}}</h3>
                            <button class="btn_insurfact waves-effect_insurfact waves-light_insurfact">Per month
                            </button>
                            <br>
                            <br>
                            <h6 class="center_insurfact white-text" for="amort">
                                Amortization period
                            </h6>
                            <div class="row_insurfact">
                                <div class="col_insurfact s12 m6 l6 offset-l3 offset-m3">
                                    <select class="browser-default_insurfact" v-model="amortization" id="amort">
                                        <option value="0" disabled>Choose amortization period</option>
                                        <option value="5">5 Años</option>
                                        <option value="10">10 Años</option>
                                        <option value="15">15 Años</option>
                                        <option value="20">20 Años</option>
                                        <option value="25">25 Años</option>
                                        <option value="30">30 Años</option>
                                    </select>
                                </div>
                            </div>
                            <br>
                        </div>
                        <h5 v-else class="white-text">You cannot calculate your budget with this data.</h5>
                    </div>
                </div>
            </div>
        </div>
        <producties v-if="!is204" :loans="loans" :amortization="amortization" :companies="companies"
                    :errored="errored" :is204="is204"
                    :loading="loading"></producties>
        <mfooter></mfooter>
    </div>
</template>

<script>
    import CryptoJS from 'crypto-js';
    import Axios from 'axios';
    import Producties from "./Producties";
    import Mheader from "./Mheader";
    import Mfooter from "./Mfooter";

    export default {
        name: "Insurfact",
        components: {Mfooter, Mheader, Producties},
        data: () => ({
            keySize: 128,
            iterationCount: 1000,
            loading: true,
            errored: false,
            err: null,
            is204: false,
            crypt_data: null,
            companies: null,
            select_term_value: 0,
            select_term_value2: '4',
            select_open_closed: 0,
            select_open_closed2: 'C',
            select_rate_type: 0,
            select_rate_type2: 'F',
            select_province: 'QC',
            minrate: 0,
            amortization: 25,
            loans: 100000
        }),
        mounted() {
            this.getData()
        },
        computed: {
            getc3: function () {
                return (this.minrate / 100) / 12
            },
            getb3: function () {
                return Math.pow(1 + this.getc3, 12 * this.amortization)
            },
            getd3: function () {
                return this.getb3 - 1
            },
            getQuote: function () {
                return Math.round(this.loans * this.getc3 * this.getb3 / this.getd3 * 100) / 100
            },
        },
        methods: {
            getData: function () {
                const uri = "https://wsemortgage.insurfact.com/wsemortgage/webresources/mortgage1/"
                let param = this.select_term_value2 + '/' + this.select_open_closed2 + '/' + this.select_rate_type2 + '/' + this.select_province + '/' + '2'
                Axios
                    .get(uri + encodeURIComponent(this.encrypt(param, 'insurfact')))
                    .then(response => {
                        if (response.status == 200) {
                            this.crypt_data = response.data.response
                            this.getValues()
                        } else if (response.status == 204) {
                            this.is204 = true
                            this.minrate = 0
                        }

                    })
                    .catch(error => {
                        this.errored = true
                        this.err = error
                    })
                    .finally(() => {
                        this.loading = false
                    })
            },
            getValues: function () {
                let array_encrypt = this.crypt_data.split(':')
                this.companies = JSON.parse(this.decrypt(array_encrypt[0], array_encrypt[1], array_encrypt[2], 'insurfact').toString())
                this.minrate = this.companies[0].interest_rate_value
            },
            onChangeValue: function () {
                if (this.select_term_value != 0) {
                    this.select_term_value2 = this.select_term_value
                }
                this.select_term_value = 0

                if (this.select_open_closed != 0) {
                    this.select_open_closed2 = this.select_open_closed
                }
                this.select_open_closed = 0

                if (this.select_rate_type != 0) {
                    this.select_rate_type2 = this.select_rate_type
                }
                this.select_rate_type = 0

                this.loading = true
                this.errored = false
                this.err = null
                this.companies = null
                this.is204 = false
                this.getData()
            },
            encrypt: function (plainText, passPhrase) {
                let iv = CryptoJS.lib.WordArray.random(this.keySize / 8).toString(CryptoJS.enc.Hex);
                let salt = CryptoJS.lib.WordArray.random(this.keySize / 8).toString(CryptoJS.enc.Hex);
                let key = this.generateKey(salt, passPhrase)
                let encrypted = CryptoJS.AES.encrypt(
                    plainText,
                    key,
                    {iv: CryptoJS.enc.Hex.parse(iv)});
                let a = encrypted.ciphertext.toString(CryptoJS.enc.Base64)
                let paramrequest = salt + ":" + iv + ":" + a;
                return (paramrequest.toString())
            },
            decrypt: function (salt, iv, encryptedText, passPhrase) {
                let key = this.generateKey(salt, passPhrase);
                let cipherParams = CryptoJS.lib.CipherParams.create({
                    ciphertext: CryptoJS.enc.Base64.parse(encryptedText)
                });
                let decrypted = CryptoJS.AES.decrypt(
                    cipherParams,
                    key,
                    {iv: CryptoJS.enc.Hex.parse(iv)});
                return decrypted.toString(CryptoJS.enc.Utf8);
            },
            generateKey: function (salt, passPhrase) {
                var key = CryptoJS.PBKDF2(
                    passPhrase,
                    CryptoJS.enc.Hex.parse(salt),
                    {keySize: this.keySize / 32, iterations: this.iterationCount});
                return key;
            }
        }
    }

</script>

<style>
    #msform .insur_input {
        background: #fff;
        padding: 15px;
        border: 1px solid #ccc;
        border-radius: 3px;
        margin-bottom: 10px;
        width: 100%;
        box-sizing: border-box;
        font-family: montserrat;
        color: rgb(21, 78, 110);
        font-size: 20px;
        font-weight: bold;
        text-align: center;
    }

    @media screen and (min-width: 993px) {
        #card_1 {
            min-height: 675px;
        }

        #card_2 {
            height: 379px;
        }
    }

    @media screen and (max-width: 1200px) {
        #years, #open, #closed, #fixed, #variable {
            font-size: large;
        }

    }
</style>