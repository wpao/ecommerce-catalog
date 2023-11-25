<template>
    <div class="container" :style="{backgroundColor: '#DCDCDC'}">
        <div class="card">
            <h3>This product is unavailable to show</h3>
            <button @click="getProduct" class="btn-next-404">Next product</button>
        </div>
    </div>
</template>

<script>
export default {
    data(){
        return {
            numericValue: null
        }
    },
    props: {
        idProduct: String
    },
    emits: ['response'],
    methods: {
        getProduct(){
            this.numericValue = parseInt(this.idProduct);
            this.$emit('response', this.numericValue)
        }
    }
}
</script>

<style scoped>

  .card {
    background-color: #FFF;
    width: 70%;
    height: 70%;
    padding: 5%;
    margin-bottom: -20%;
    border-radius: 6px;
    box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.1);

    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }

  .btn-next-404 {
    width: 50%;
    height: 10%;
    border: 1px solid #000000;
    color: #000000;
    border-radius: 4px;
    cursor: pointer;
  }

</style>
