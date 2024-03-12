<template>
    <div class="ConversorComponente">
        <h2>{{ moedaA }} Para {{ moedaB }}</h2>
        <input type="text" v-model="moedaA_value" v-bind:placeholder="moedaA">
        <input type="button" value="Converter" v-on:click="converter()">
        <h2>{{ moedaB_value }}</h2>
    </div>
</template>

<script>
export default {
    name: 'ConversorComponente',
    props: ["moedaA", "moedaB"],
    data() {
        return {
            moedaA_value: "",
            moedaB_value: 0,
            cotacao: {} // Propriedade para armazenar a cotação
        }
    },
    methods: {
        converter() {
            let de_para = this.moedaA + "-" + this.moedaB;
            let de_para_json = this.moedaA + this.moedaB;
            let url = "https://economia.awesomeapi.com.br/last/" + de_para;

            fetch(url)
                .then(res => {
                    if (!res.ok) {
                        throw new Error('Erro ao buscar cotação: ' + res.status);
                    }
                    return res.json();
                })
                .then(json => {
                    const cotacao = json[de_para_json]; // Acessar a cotação dentro de USDBRL
                    if (cotacao && cotacao.ask !== undefined) {
                        this.moedaB_value = cotacao.ask * parseFloat(this.moedaA_value);
                    } else {
                        throw new Error('Resposta da API inválida ou dados de cotação ausentes');
                    }
                })
                .catch(error => {
                    console.error(error);
                });
        }
    }
};
</script>

<style scoped>

</style>