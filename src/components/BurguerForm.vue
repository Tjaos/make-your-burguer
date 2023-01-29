<template>
    <div>
        <p>Componente de Mensagem</p>
        <div>
            <form id="burguer-form" @submit="createBurger">
                <div class="input-container">
                    <label for="nome">Nome do Cliente</label>
                    <input type="text" id="nome" name="name" v-model="nome" placeholder="Digite seu nome">
                </div>
                <div class="input-container">
                    <label for="pao">Tipo do pão</label>
                    <select name="pao" id="pao" v-model="pao">
                        <option value="">Selecione o seu pão</option>
                        <option v-for="pao in paes" :key="pao.id" :value="pao.tipo">
                            {{pao.tipo}}
                        </option> 
                    </select>
                </div>
                <div class="input-container">
                    <label for="carne">Tipo da Carne do seu burguer</label>
                    <select name="carne" id="carne" v-model="carne">
                    <option value="">Escolha o tipo de carne</option>
                    <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo">
                            {{ carne.tipo }}
                    </option> 
                </select>
                </div>

                <div id="opcionais-container" class="input-container">
                    <label for="opcionais" id="opcionais-title">Selecione os opcionais</label>
                    <div class="checkbox-container" v-for="opcional in opcionaisdata" :key="opcional.id">
                        <input type="checkbox" name="opcionais" v-model="opcionais" :value="opcional.tipo">
                        <span>{{ opcional.tipo }}</span>
                    </div>
                </div>


                <div class="input-container">
                    <input type="submit" class="submit-btn" value="Criar meu Burguer!">
                </div>
            </form>
        </div>
    </div>
</template>

<script>
export default {
    name: "BurguerForm",
    data(){
        return{
//dados que virão do servidor
           paes: null,
           carnes: null,
           opcionaisdata: null,
//dados que serão enviados
           nome: null,
           pao: null,
           carne:null,
           opcionais: [],
           msg: null
        }
    },
    methods:{
        async getIngredientes(){
            const req = await fetch("http://localhost:3000/ingredientes");
            const data = await req.json();

            this.paes = data.paes;
            this.carnes = data.carnes;
            this.opcionaisdata = data.opcionais;
        },
        async createBurger(e){
           e.preventDefault();
           
           const data ={
            nome: this.nome,
            carne: this.carne,
            pao: this.pao,
            //adicionando os dados num array
            opcionais: Array.from(this.opcionais),
            status: "Solicitado"
           }

           const dataJson = JSON.stringify(data);

           const req = await fetch("http://localhost:3000/burgers",{
                method: "POST",
                headers: { "Content-type": "application/json" },
                body: dataJson
           });

           const res = await req.json();

           //mandar uma msg ao sistema

           //limpar msg da tela

           //limpar os campos
           this.nome = "";
           this.carne="";
           this.pao="";
           this.opcionais="";
        }
    },
    mounted(){
        this.getIngredientes()
    }
}
</script>

<style scoped>
    #burguer-form{
        max-width: 400px;
        margin: 0 auto;
    }
    .input-container{
        display: flex;
        flex-direction: column;
        margin-bottom: 20px;
    }

    label{
        font-weight: bold;
        margin-bottom: 15px;
        color: #222;
        padding: 5px 10px;
        border-left: 4px solid #FCBA03;
    }

    input, select{
        padding: 5px 10px;
        width: 300px;
    }

    #opicionais-container{
        flex-direction:row;
        flex-wrap: wrap;
    }

    #opicionais-title{
        width: 100%;
    }

    .checkbox-container{
        display: flex;
        align-items: flex-start;
        width: 50%;
        margin-bottom: 20px;
    }

    .checkbox-container span, 
    .checkbox-container input{
        width: auto;
    }

    .checkbox-container span{
        margin-left:6px;
        font-weight: bold;
    }

    .submit-btn{
        background-color: #222;
        color: #FCBA03;
        font-weight: bold;
        border: 2px solid #222;
        padding: 10px;
        font-size: 16px;
        margin: 0 auto;
        cursor:pointer;
        transition: .5s;
    }

    .submit-btn:hover{
        background-color: transparent;
        color: #222;
    }
</style>