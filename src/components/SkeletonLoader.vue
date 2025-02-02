<script>
export default {};
</script>
<template lang="">
  <div class="container">
    <div class="skeleton-img"></div>
    <div class="skeleton-content">
      <div class="skeleton-header">
        <h1 class="skeleton-title"></h1>
        <div class="skeleton-information">
          <span class="skeleton-category"></span>
          <div class="skeleton-rating">
            <div></div>
            <span v-for="index in 5" :key="index"></span>
          </div>
        </div>
      </div>
      <p v-for="index in 5" :key="index"></p>
      <div class="skeleton-content-footer">
        <h1 class="skeleton-price"></h1>
        <div class="btn">
          <button></button>
          <button></button>
        </div>
      </div>
    </div>
  </div>
</template>
<style scoped>
.container {
  display: grid;
  grid-template-columns: 1.4fr 2fr;
  align-items: center;
  gap: 50px;
  height: 100%;
}

.skeleton-img {
  width: 100%;
  height: 100%;
  animation: pulse 2s linear infinite alternate;
}

.skeleton-content {
  position: relative;
  width: 100%;
  height: 100%;
}

.skeleton-title {
  width: 100%;
  height: 30px;
  animation: pulse 2s linear infinite alternate;
}

.skeleton-information {
  display: flex;
  justify-content: space-between;
  padding: 11px 0;
  border-bottom: 1px solid #00000033;
}

.skeleton-category {
  width: 100px;
  height: 20px;
  animation: pulse 2s linear infinite alternate;
}

.skeleton-rating {
  display: flex;
  gap: 3px;
}

.skeleton-rating div {
  width: 50px;
  height: 20px;
  animation: pulse 2s linear infinite alternate;
}

.skeleton-rating span {
  width: 20px;
  aspect-ratio: 1;
  border-radius: 50%;
  animation: pulse 2s linear infinite alternate;
}

p {
  width: 100%;
  height: 20px;
  animation: pulse 2s linear infinite alternate;
}

.skeleton-content-footer {
  position: absolute;
  bottom: 0;
  border-top: 1px solid #00000033;
}

.skeleton-price {
  width: 100px;
  height: 20px;
  margin-top: 20px;
  animation: pulse 2s linear infinite alternate;
}

button {
  width: full;
  height: 40px;
  margin: 10px 0;
  animation: pulse 2s linear infinite alternate;
}

@keyframes pulse {
  0% {
    background-color: var(--secondary-color);
    opacity: 0.3;
  }
  100% {
    background-color: var(--secondary-color);
    opacity: 1;
  }
}
</style>
