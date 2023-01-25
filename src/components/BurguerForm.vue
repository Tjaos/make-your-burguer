<template>
    <div>
        <p>Componente de Mensagem</p>
        <div>
            <form id="burguer-form">
                <div class="input-container">
                    <label for="nome">Nome do Cliente</label>
                    <input type="text" id="nome" name="name" v-model="nome" placeholder="Digite seu nome">
                </div>
                <div class="input-container">
                    <label for="pao">Tipo do pão</label>
                    <select name="pao" id="pao" v-model="pao">
                        <option value="">Selecione o seu pão</option>
                        <option value="integral">Integral</option> 
                    </select>
                </div>
                <div class="input-container">
                    <label for="carne">Tipo da Carne do seu burguer</label>
                    <select name="carne" id="carne" v-model="carne">
                    <option value="">Escolha o tipo de carne</option>
                    <option value="maminha">Maminha</option> 
                </select>
                </div>
                <div id="opicionais-container" class="input-container">
                    <label for="opicionais" id="opicionais-title">Selecione os opicionais</label>
                    <div class="checkbox-container">
                        <input type="checkbox" name="opicionais" v-model="opicionais" value="salame">
                        <span>Salame</span>
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
    name: "BurguerForm"
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