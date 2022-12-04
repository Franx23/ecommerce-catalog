<template>
  <body>
    <div class="centered"><div class="loader"></div></div>
    <div
      v-if="!loading"
      :class="
        products.category == 'men\'s clothing' ? 'Page-man' : 'Page-woman' &&
        products.category == 'women\'s clothing' ? 'Page-woman' : 'Page-man' &&
        products.category == 'electronics' ? 'Page-unvailable' : 'Page-unvailable'">
      <div class="Page-img"><img :src="texture" /></div>
      <div
        v-if="
          products.category == 'men\'s clothing' ||
          products.category == 'women\'s clothing'
        "
      >
        <div id="card">
          <div class="box-image">
            <img :src="products.image" height="400" width="300" align="right" />
          </div>
          <div class="box">
            <h2 :class="products.category == 'men\'s clothing' ? 'title-men' : 'title-women'">{{ products.title }}</h2>
            <h3>{{ products.category }}</h3>
            <div class="rating">
              <h4>{{ products.rating.rate }}/5</h4>
              <div class="rating-box">
                <span :class="products.category == 'men\'s clothing' ? 'circle-men': 'circle-women'"></span>
                <span :class="products.category == 'men\'s clothing' ? 'circle-men': 'circle-women'"></span>
                <span :class="products.category == 'men\'s clothing' ? 'circle-men': 'circle-women'"></span>
                <span :class="products.category == 'men\'s clothing' ? 'circle-men-border' : 'circle-women-border'"></span>
                <span :class="products.category == 'men\'s clothing' ? 'circle-men-border' : 'circle-women-border'"></span>
              </div>
            </div>
            <div class="line"></div>
            <p>{{ products.description }}</p>
            <div class="line2"></div>
            <h5 :class="products.category == 'men\'s clothing' ? 'price-men' : 'price-women'">${{ products.price }}</h5>
            <div class="button">
              <button :class="products.category == 'men\'s clothing' ? 'button-buy-men' : 'button-buy-women'">Buy Now</button>
              <button :class="products.category == 'men\'s clothing' ? 'button-next-men': 'button-next-women'" @click.prevent="Nextbutton()">Next Product</button>
            </div>
          </div>
        </div>
      </div>

      <div v-else>
        <div id="card-unvailable">
          <h1>This product is unavailable to show</h1>
          <button class="unvailable-btn" @click.prevent="Nextbutton()">Next Product</button>
        </div>
      </div>
    </div>
  </body>
</template>
  
  <script>
export default {
  data() {
    return {
      products: [],
      index: 1,
      loading: true,
      texture: require("../assets/Texture.png"),
    };
  },
  methods: {
  async fetchData() {
    const response = await fetch("https://fakestoreapi.com/products/" + this.index);
      const data = await response.json();
      this.loading = false;
      this.products = data;
    },
    Nextbutton() {
      if (this.index < 20) {
        this.index++;
        this.fetchData();
      } else {
        this.index = 1;
      }
      console.log(this.index);
    },
  },
  created() {
    this.loading = true;
    this.fetchData();
  },
};
</script>
  
  <style>
  
  
  </style>
  