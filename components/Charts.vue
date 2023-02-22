<template>
    <b-container align-h="center" align-v="center" class="bg-dark">
        <b-row  align-v="center" v-for="(coins, index) in cryptoCoins" :key="index" :value="coins" class="text-light">
            <b-col align-self="center">
                <h4>
                {{ coins }}
                </h4> 
            </b-col>
            <b-col >
                <p>
                  Low: {{ priceLow[index] }}  
                </p>
            </b-col>
            <b-col>
                <p>
                  High: {{ priceHigh[index] }}   
                </p>
            </b-col>
        </b-row>
    </b-container>
</template>
 

<style>

</style>

<script>
    export default({
          data() {
            return {
                cryptoCoins: [],
                cryptoCoinsID: [],
                priceHigh: [],
                priceLow: []
            };
        },
        async mounted(){
            fetch('https://api.coinpaprika.com/v1/coins/')
            .then((response) => response.json())
            .then((data) => {
                // console.log(data)
                const cryptoCoins = this.cryptoCoins
                const cryptoCoinsID = this.cryptoCoinsID
                const priceHigh = this.priceHigh
                const priceLow =  this.priceLow
                const coinArray = data.slice(0,10);
                for (let index=0; index < coinArray.length; index++){
                    cryptoCoins.push(coinArray[index].name);
                    cryptoCoinsID.push(coinArray[index].id);
                    //console.log(cryptoCoins);
                    fetch('https://api.coinpaprika.com/v1/coins/' + cryptoCoinsID[index] + '/ohlcv/latest')
                    .then((response) => response.json())
                    .then((data) => {
                        priceHigh.push(data[0].high)
                        priceLow.push(data[0].low)
                    })
                    //console.log(priceHigh)
                }
            
                
                //cryptoCoins.for(coins in cryptoCoins)
                // this.cryptoCoins.push(topTenCoins);
                //;
            })
            
            
            
        }
    })

    
</script>