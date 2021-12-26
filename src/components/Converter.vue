<template>
  <div class="converter">
    <h2>{{ coinA }} para {{ coinB }}</h2>
    <input type="text" v-model="coinA_value" :placeholder="coinA">
    <input type="button" value="Converter" @click="toConverter">
    <h2>{{ coinB_value }}</h2>
  </div>
</template>

<script>
export default {
    name: "Converter",
    props: ["coinA", "coinB"],
    data() {
        return {
            coinA_value: "",
            coinB_value: 0,
        }
    },
    methods: {
        toConverter(){
            let from_to = this.coinA + "_" + this.coinB;
            let url = "https://free.currconv.com/api/v7/convert?q=" + from_to + "&compact=ultra&apiKey=f40f63f983ef4c9280a9";
            fetch(url).then(res => { 
                return res.json();
            }).then(json => {
                // console.log(json)
                let cotation = json[from_to];
                this.coinB_value = (cotation * parseFloat(this.coinA_value)).toFixed(2);
            });
        }
    }
};
</script>

<style scoped></style>
