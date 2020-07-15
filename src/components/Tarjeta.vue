<template>
    <div class="col_insurfact s12 m4 l3">
        <div class="card_insurfact center_insurfact">
            <div class="card_insurfact-content">
                <h6 class="truncate_insurfact" s>{{ company.company_desc_en }}</h6>
                <span style="font-weight: bold; font-size: 20px"> {{ company.interest_rate_value }} % </span>
                <p >$ {{getQuote2}}</p>
                <br>
                <button class="btn_insurfact btn-small_insurfact" style="background-color: rgb(39, 89, 195)">View Rates</button>

            </div>
        </div>
    </div>

</template>

<script>
    export default {
        name: "Tarjeta",
        props: ['company', 'quote', 'amortization', 'loans'],
        computed: {
            getQuote2: function () {
                const c3 = (this.company.interest_rate_value / 100) / 12
                const b3 = Math.pow(1 + c3, 12 * this.amortization)
                const d3 = b3 - 1
                return Math.round(this.loans * c3 * b3 / d3 * 100) / 100
            }
        }
    }
</script>