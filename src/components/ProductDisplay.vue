<script>
import SkeletonLoader from "./SkeletonLoader.vue";
export default {
  components: { SkeletonLoader },
  data() {
    return {
      product: null,
      indexProduct: 1,
      simplifiedCategory: "",
      isLoading: true,
    };
  },
  methods: {
    async getDataAPI(index) {
      try {
        this.isLoading = true;
        const response = await fetch(
          `https://fakestoreapi.com/products/${index}`
        );
        const data = await response.json();
        if (
          data.category === "men's clothing" ||
          data.category === "women's clothing"
        ) {
          this.product = data;
          this.simplifiedCategory =
            data.category === "men's clothing" ? "mens" : "womens";
        } else {
          this.product = null;
          this.simplifiedCategory = "blank";
        }
      } catch (error) {
        console.error(error);
      } finally {
        this.isLoading = false;
      }
    },

    nextProduct() {
      this.indexProduct < 20 ? this.indexProduct++ : (this.indexProduct = 1);
      this.getDataAPI(this.indexProduct);
    },
  },
  created() {
    this.getDataAPI(this.indexProduct);
  },
};
</script>

<template>
  <div
    class="background"
    :class="`${
      isLoading
        ? 'blank-background-theme'
        : `${simplifiedCategory}-background-theme`
    }`"
  >
    <div class="card-product">
      <SkeletonLoader v-if="isLoading" />
      <!-- Product found -->
      <div class="found" v-else-if="product">
        <img :src="product.image" :alt="product.title" />
        <div class="content">
          <div class="content-header">
            <h1 :class="`${simplifiedCategory}-font-color`">
              {{ product.title }}
            </h1>
            <div class="information">
              <span class="category">{{ product.category }}</span>
              <div class="rating">
                <span>{{ product.rating.rate }}/5</span>
                <div class="rating-icons">
                  <span
                    v-for="index in 5"
                    :key="index"
                    :class="
                      index <= Math.round(product.rating.rate)
                        ? `${simplifiedCategory}-rating-icon`
                        : 'blank'
                    "
                  >
                  </span>
                </div>
              </div>
            </div>
          </div>
          <p>{{ product.description }}</p>
          <div class="content-footer">
            <h1 class="price" :class="`${simplifiedCategory}-font-color`">
              {{
                product.price.toLocaleString("en-US", {
                  style: "currency",
                  currency: "USD",
                })
              }}
            </h1>
            <div class="btn">
              <button :class="`${simplifiedCategory}-btn-buy-now`">
                Buy Now
              </button>
              <button
                :class="`${simplifiedCategory}-btn-next-product`"
                @click="nextProduct"
              >
                Next Product
              </button>
            </div>
          </div>
        </div>
      </div>

      <!-- Product not found -->
      <div class="not-found" v-else>
        <span>This product is unavailable to show</span>
        <button class="blank-btn-next-product" @click="nextProduct">
          Next Product
        </button>
      </div>
    </div>
  </div>
</template>
<style></style>
