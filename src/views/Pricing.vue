<template>
  <div class="flex justify-center flex-col items-center">
    <div class="w-1/2 bg-blue-900 rounded-lg shadow px-6 py-12 flex flex-col items-center">
      <div class="bg-gray-400 rounded-full flex justify-around p-1">
        <button v-for="(price , frequency) in plans[0].pricing"   @click="currentFrequency= frequency" class="rounded-full text-xs font-bold px-6 py-1 uppercase focus:outline-none" :class="currentFrequency == frequency ? 'bg-blue-900 text-white' : ''">{{ frequency }}</button>
      </div>
      <div class="pt-8 flex w-full ">
        <div v-for="plan in plans" :key="plan.id" class="text-white w-1/2">
          <h1 v-text="plan.name" class="text-2xl font-bold"></h1>
          <ul class="pt-4">
            <li v-for="benefit in plan.benefits[currentFrequency]">{{ benefit }}</li>
          </ul>
          <div class="flex justify-center pt-8">
            <div class="text-4xl font-bold">{{ getPrice(plan.pricing[currentFrequency].price) }}</div>
            <div class="pl-2 pt-2 text-gray-300">{{ plan.pricing[currentFrequency].label }}</div>
          </div>
        </div>
      </div>
      <div class="pt-4 text-center text-gray-400 text-sm font-bold">
        <a href="#" @click.prevent="currency = 'usd'">USD</a> |
        <a href="#" @click.prevent="currency = 'eur'">EUR</a> |
        <a href="#" @click.prevent="currency = 'inr'">INR</a>
      </div>
    </div>
    <div class="text-gray-500"><a href="https://github.com/Itxshakiil/Pricing-Table-in-Vue">View Code</a> </div>
  </div>
</template>

<script>
export default {
  name: "Pricing",
  methods: {
    getPrice:function(price){
      return this['currency' + this.currency.toUpperCase()](price);
    },
    currencyUSD:function(price){
      return '$' + price;
    },
    currencyEUR:function(price){
      return  Math.ceil(price * 0.85) + "€"
    },
    currencyINR:function(price){
      return  Math.ceil(price * 70) + "₹"
    },
  },
  data() {
      return {
          currentFrequency:'monthly',
          currency:'usd',
          plans : [
            { id:1,
              name:'Starter',
              benefits:{
                monthly:['Benefit 1','Benefit 2','Benefit 2'],
                yearly:['Benefit 1','Benefit 2','Benefit 3','Benefit 4'],
                lifetime:['Benefit 1','Benefit 2','Benefit 3','Benefit 4','Benefit 5',],
              },
              pricing:{
                monthly:{price:99,label:'/mo'},
                yearly:{price:499,label:'/yr'},
                lifetime:{price:1200,label:''},
              }
            },{
              id:2,
              name:'Pro',
              benefits:{
                monthly:['Benefit 1','Benefit 2','Benefit 2'],
                yearly:['Benefit 1','Benefit 2','Benefit 3','Benefit 4'],
                lifetime:['Benefit 1','Benefit 2','Benefit 3','Benefit 4','Benefit 5',],
              },
              pricing:{
                monthly:{price:199,label:'/mo'},
                yearly:{price:799,label:'/yr'},
                lifetime:{price:2200,label:''},
              }
            },{
              id:3,
              name:'Enterprise',
              benefits:{
                monthly:['Benefit 1','Benefit 2','Benefit 2'],
                yearly:['Benefit 1','Benefit 2','Benefit 3','Benefit 4'],
                lifetime:['Benefit 1','Benefit 2','Benefit 3','Benefit 4','Benefit 5',],
              },
              pricing:{
                monthly:{price:499,label:'/mo'},
                yearly:{price:999,label:'/yr'},
                lifetime:{price:2999,label:''},
              }
            }
          ]
      }
  },
};
</script>

<style>
</style>