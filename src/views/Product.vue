<template>
  <div class="product">
    <HeaderCandleshine />
    
      <!-- Breadcrumb Section Begin -->
    <div class="breacrumb-section">
        <div class="container">
            <div class="row">
                <div class="col-lg-12">
                    <div class="breadcrumb-text product-more text-left">
                        <router-link to="/"><i class="fa fa-home"></i> Home</router-link>
                        <span>Detail</span>
                    </div>
                </div>
            </div>
        </div>
    </div>
    <!-- Breadcrumb Section Begin -->

    <!-- Product Shop Section Begin -->
    <section class="product-shop spad page-details">
        <div class="container">
            <div class="row">
                <div class="col-lg-12">
                    <div class="row">
                        <div class="col-lg-6">
                            <div class="product-pic-zoom">
                                <img class="product-big-img" :src="gb_default" alt="" />
                            </div>
                            <div class="product-thumbs" v-if="productDetails.galleries.length > 0">
                                <carousel class="product-thumbs-track ps-slider" :dots="false" :nav="false">
                                    <div v-for="ss in productDetails.galleries"
                                    :key="ss.id"
                                    class="pt" @click="ChangeImage(ss.photo)" :class="ss.photo==gb_default ? 'active':'' ">
                                        <img :src="ss.photo" alt="" />
                                    </div>

                                </carousel>
                            </div>
                        </div>
                        <div class="col-lg-6">
                            <div class="product-details text-left">
                                <div class="pd-title">
                                    <span>{{ productDetails.type}}</span>
                                    <h3>{{ productDetails.name}}</h3>
                                </div>
                                <div class="pd-desc">
                                    <p v-html="productDetails.description"></p>
                                    <h4>Rp.{{ productDetails.price}}</h4>
                                </div>
                                <div class="quantity">
                                    <!-- <router-link to="/cart"> -->
                                        <a @click="saveKeranjang(productDetails.id,productDetails.name, productDetails.price, productDetails.galleries[0].photo)" href="#" class="primary-btn pd-cart">Add To Cart</a>
                                    <!-- </router-link> -->
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>
    <!-- Product Shop Section End -->

    <RelatedProduct />
    <FooterCandleshine />
    
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'
import HeaderCandleshine from '@/components/HeaderCandleshine.vue'
import FooterCandleshine from '../components/FooterCandleshine.vue'
import RelatedProduct from '../components/RelatedProduct.vue'
import carousel from 'vue-owl-carousel'
import axios from 'axios'


export default {
  name: 'Product',
  components: {
    HeaderCandleshine,
    FooterCandleshine,
    carousel,
    RelatedProduct
  },
  data(){
    return {
      gb_default: "",
      productDetails: [],
      keranjangUSer : []
    }
  },
  methods: {
    ChangeImage(urlImage){
      this.gb_default = urlImage;
    },
    setDataPicture(data){
        //replace object productDetails dengan data dari API
        this.productDetails = data;

        //replace value gambar default
        this.gb_default = data.galleries[0].photo

    },
    saveKeranjang(idProduct,nameProduct, priceProduct, photoProduct){
        var productStore={
            "id" : idProduct,
            "name" : nameProduct,
            "price" : priceProduct,
            "photo" : photoProduct,

        }
        this.keranjangUSer.push(productStore);
        const parsed = JSON.stringify(this.keranjangUSer);
        localStorage.setItem('keranjangUSer', parsed);
    }
  },
  mounted(){
        if (localStorage.getItem('keranjangUSer')) {
            try {
                this.keranjangUSer = JSON.parse(localStorage.getItem('keranjangUSer'));
            } catch(e) {
                localStorage.removeItem('keranjangUSer');
            }
        }
        axios
        .get("http://127.0.0.1:8000/api/products",{
            params:{
                id: this.$route.params.id
            }
        })
        .then(res =>(this.setDataPicture(res.data.data)))
        // eslint-disable-next-line no-console
        .catch(err=>console.log(err));
    }
}
</script>

<style>
  .product-thumbs .pt{
    margin-right: 14px;
  }
</style>
