<script>
import { parse } from '@vue/compiler-dom';

export default {
    data() {
        return {
            cardNumberValue: '',
            userName: '',
            expDateYear: '',
            expDateMonth: '',
            cvc: ''
        }
    },
    computed: {
        formatCardNumber() {
            let numbersOnly = this.cardNumberValue.replace(/\D/g, '');
            this.cardNumberValue = numbersOnly.replace(/(\d{4})(?=\d)/g, '$1 ');
        },
        parseYear(){
            if (!isNaN(this.expDateYear) && this.expDateYear !== '') {
                this.expDateYear = this.expDateYear.replace(/[^0-9]/g, '').slice(0, 2)
                if (this.expDateYear <= 0){
                    this.expDateYear = 1
                } else if (this.expDateYear > 99){
                    this.expDateYear = 99
                }
            } else {
                this.expDateYear = "00"
            }
        },
        parseMonth(){
            if (!isNaN(this.expDateMonth) && this.expDateMonth !== '') {
                this.expDateMonth = this.expDateMonth.replace(/[^0-9]/g, '').slice(0, 2)
                if (this.expDateMonth <= 0){
                    this.expDateMonth = 1
                } else if (this.expDateMonth > 12){
                    this.expDateMonth = 12
                }
            } else {
                this.expDateMonth = "00"
            }
        },
        parseCVC(){
            if (this.cvc.length > 3){
                this.cvc = this.cvc.slice(0,3 )
            }
        }
    }
}

</script>

<template>
    <div>
        <div class="card">
            <div class="circles">
                <div class="fullCircle"></div>
                <div class="circle"></div>
            </div>
            <h3>{{ cardNumberValue.length > 0 ? cardNumberValue : 'XXXX XXXX XXXX XXXX' }}</h3>
            <h4>NAME: {{userName}}</h4>
            <h4>EXP: {{expDateMonth.length > 0 ? expDateMonth : "00"}}/{{expDateYear.length > 0 ? expDateYear : "00"}}</h4>
            <h4>CVC: {{cvc.length > 0 ? cvc : "XXX"}}</h4>
        </div>
        <form action="#" id="cardInputs">
            <div>
                <label for="name">Cardholder name</label>
                <input type="text" name="" id="name" v-model="userName">
            </div>

            <div>
                <label for="cardNumber">Card number</label>
                <input type="text" name="" maxlength="19" id="cardNumber" @input="formatCardNumber" v-model="cardNumberValue">
            </div>

            <div>
                <label for="">Exp date (MM/YY)</label>
                <input type="text" name="" id="month" v-model="expDateMonth" @input="parseMonth" >
                <input type="text" name="" id="year"  v-model="expDateYear" @input="parseYear">
            </div>
            <div>

                <label for="cvc">CVC</label>
                <input type="text" name="" id="cvc" v-model="cvc" @input="parseCVC">
            </div>

            <input type="submit" value="Confirm">
        </form>
    </div>
</template>

<style scoped>
body{
    width: 100%;
    min-height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
}

#cardInputs{
    display: flex;
    flex-direction: column;
    gap: 20px;
}

#cardInputs label{
    display: block;
}

#cardInputs>div:nth-child(3){
    display: flex;
    gap: 20px;
}

#cardInputs>div>input{
    width: 100%;
    box-sizing: border-box;
}

#cardInputs>div:nth-child(3)>div:first-child input{
    width: 50px;
}



input[type="submit"]{
    background-color: black;
    color: white;
}


.card{
    background: linear-gradient(to right, rgb(116, 116, 233), rgb(187, 19, 187));
    color: white;
}

.circles{
    display: flex;
    align-items: center;
}

.fullCircle{
    border: 1px solid white;
    width: 30px;
    height: 30px;
    border-radius: 50%;
    background-color: white;
    margin-right: 10px;
}
.circle{
    border: 1px solid white;
    width: 15px;
    height: 15px;
    border-radius: 50%;
}

</style>
