<script>
import Loader from './Loader.vue'
import NotePound from './NotePound.vue'

export default {
  components: {
    'Loader': Loader,
    'NotePound': NotePound
  },
  data() {
    return {
        product: '',           // data untuk di tampilkan
        id: 1,                 // acuan mencari data
        backgroundColor: '',   // color background, nilai default di set untuk tampilan 404
        colorText: '',         // color text, nilai default di set untuk tampilan 404
        error: false,          // Error handling
        btnNext: ''
    }
  },
  methods: {
    async getProduct(id){
      try {
        // set error untuk mengatur togle template card
        this.error = false;

        // fatch data berdasarkan index from API
        let response = await fetch("https://fakestoreapi.com/products/"+this.id)
        let product = await response.json()

        // set data ke product
        this.product = product

        // set dua color 
        // this.backgroundColor = product.category === "men's clothing" ? '#D6E6FF' : '#FDE2FF';
        // this.colorText = product.category === "men's clothing" ? '#002772' : '#720060';

        // set 3 color, dikarnakan button style
        if( product.category === "men's clothing" ){
          this.backgroundColor = '#D6E6FF'
          this.colorText = '#002772'
          this.btnNext = 'btn-next-man'
        } else if ( product.category === "women's clothing" ) {
          this.backgroundColor = '#FDE2FF'
          this.colorText = '#720060'
          this.btnNext = 'btn-next-woman'
        } else {
          this.backgroundColor = '#DCDCDC'
          this.colorText = 'black'
          this.btnNext = 'btn-next-404'
        }

      } catch (error){
        this.id = 1         // reset fetch API product
        this.error = true;  // kondisi toggle page note pound(404)
      }
    }
  },
  mounted(){
    // menjalankan method
    this.getProduct()
  },
}
</script>

<template>
    <div v-if="error">
      <NotePound @response="getProduct" idProduct='0' />
    </div>
    <div v-else>
      <div v-if="product">       
        <div class="container" :style="{backgroundColor: backgroundColor}">
          <div class="card">
            <div class="gambar">
              <img :src="product.image" alt="" width="200" height="300">
            </div>
            <div>
              <h1 :style="{color: colorText}">{{ product.title }}</h1>
              <h5>{{ product.category }}</h5>
              <hr>
              <p>{{ product.description }}</p>
              <hr>
              <h3 :style="{color: colorText}">$ {{ product.price }}</h3>
              <div class="btn">
                <button :style="{backgroundColor: colorText}" class="btn-buy">Buy now</button>
                <button :class=btnNext @click="getProduct(id++)">Next product</button>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div v-else>
        <div class="loader">
          <Loader />
          <h1>Loading...</h1>
        </div>
      </div>
    </div>
</template>