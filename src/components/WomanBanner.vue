<template>
  <section class="women-banner spad">
    <div class="container-fluid">
      <div class="row">
        <div class="col-lg-12 mt-5" v-if="products.length > 0">
          <carousel
            class="product-slider"
            :autoplay="true"
            :nav="false"
            :dots="false"
          >
            <div
              class="product-item"
              v-for="itemProduct in products"
              v-bind:key="itemProduct.id"
            >
              <div class="pi-pic">
                <img
                  v-bind:src="
                    itemProduct.galleries.length
                      ? itemProduct.galleries[0].photo
                      : ''
                  "
                  alt="xxx"
                />
                <ul>
                  <li class="w-icon active">
                    <!-- <router-link to="/cart"> -->
                    <a
                      @click="
                        saveKeranjang(
                          itemProduct.id,
                          itemProduct.name,
                          itemProduct.price,
                          itemProduct.galleries[0].photo
                        )
                      "
                      href="#"
                      ><i class="icon_bag_alt"></i
                    ></a>
                    <!-- </router-link> -->
                  </li>
                  <li class="quick-view">
                    <router-link v-bind:to="'/product/' + itemProduct.id">
                      + Quick View</router-link
                    >
                  </li>
                </ul>
              </div>
              <div class="pi-text">
                <div class="catagory-name">{{ itemProduct.type }}</div>
                <a href="#">
                  <h5>{{ itemProduct.name }}</h5>
                </a>
                <div class="product-price">
                  ${{ itemProduct.price }}
                  <span>$35.00</span>
                </div>
              </div>
            </div>
          </carousel>
        </div>
        <div class="col-lg-12" v-else>Produk belum tersedia saat ini</div>
      </div>
    </div>
  </section>
</template>
<script>
import carousel from "vue-owl-carousel";
import axios from "axios";

export default {
  name: "WomanBanner",
  components: {
    carousel,
  },
  data() {
    return {
      products: [],
      keranjangUser: [],
    };
  },
  methods: {
    saveKeranjang(idProduct, nameProduct, priceProduct, photoProduct) {
      var productStored = {
        id: idProduct,
        name: nameProduct,
        price: priceProduct,
        photo: photoProduct,
      };

      this.keranjangUser.push(productStored);
      const parsed = JSON.stringify(this.keranjangUser);
      localStorage.setItem("keranjangUser", parsed);

      window.location.reload();
    },
  },
  mounted() {
    if (localStorage.getItem("keranjangUser")) {
      try {
        this.keranjangUser = JSON.parse(localStorage.getItem("keranjangUser"));
      } catch (e) {
        localStorage.removeItem("keranjangUser");
      }
    }
    axios
      .get("http://localhost:9000/api/products")
      .then((res) => {
        this.products = res.data.data.data;
        console.log("product", this.products);
      })
      .catch((err) => console.log(err));
  },
};
</script>

<style scoped>
.product-item {
  margin: 25px;
}
</style>
