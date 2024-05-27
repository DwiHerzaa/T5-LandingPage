<template>
  <q-layout view="hHh lpR fFf">
    <!-- Header -->
    <q-header elevated class="bg-primary text-white" height-hint="98">
      <q-toolbar>
        <q-btn dense flat round icon="menu" @click="leftDrawerOpen = !leftDrawerOpen" />
        <q-toolbar-title>
          <q-avatar>
            <img src="https://www.svgrepo.com/show/477014/shopping-cart.svg" alt="Shopping Cart" />
          </q-avatar>
          Shopping-in Aja
        </q-toolbar-title>      
      </q-toolbar>
      <q-tabs align="left" class="q-mt-sm">
        <q-route-tab to="/page1" label="Beranda" />
        <q-route-tab to="/page2" label="Top Seller" />
        <q-route-tab to="/page3" label="About Me" />
      </q-tabs>
    </q-header>

    <!-- Navbar -->
    <q-drawer show-if-above v-model="leftDrawerOpen" side="left" bordered>
      <q-scroll-area class="fit">
        <q-list padding class="menu-list">
          <q-item clickable v-ripple>
            <q-item-section avatar>
              <q-icon name="inbox" />
            </q-item-section>
            <q-item-section>Inbox</q-item-section>
          </q-item>
          <q-item clickable v-ripple>
            <q-item-section avatar>
              <q-icon name="star" />
            </q-item-section>
            <q-item-section>Star</q-item-section>
          </q-item>
          <q-item clickable v-ripple>
            <q-item-section avatar>
              <q-icon name="send" />
            </q-item-section>
            <q-item-section>Send</q-item-section>
          </q-item>
          <q-item clickable v-ripple>
            <q-item-section avatar>
              <q-icon name="drafts" />
            </q-item-section>
            <q-item-section>Drafts</q-item-section>
          </q-item>
        </q-list>
      </q-scroll-area>
    </q-drawer>

    <!-- Page Content -->
    <q-page-container>
      <q-page padding class="q-pa-md">
        <!-- Carousel -->
        <q-carousel
          v-model="slide"
          arrows
          infinite
          animated
          control-color="black"
          swipeable
          transition-prev="slide-right"
          transition-next="slide-left"
          height="550px"
          class="bg-dark text-white shadow-2 rounded-borders"
        >
          <q-carousel-slide
            v-for="(image, index) in carouselImages"
            :key="index"
            :name="index"
            :img-src="image"
            class="carousel-slide"
          />
        </q-carousel>

        <!-- Cards -->
        <div class="q-mt-xl row justify-center">
          <transition-group name="fade" tag="div" class="row justify-center">
            <q-card
              v-for="product in products"
              :key="product.name"
              class="my-card q-mb-xl q-pa-md col-xs-12 col-sm-6 col-md-4 col-lg-3"
            >
              <q-img :src="product.image" :alt="product.name" class="my-card-img">
                <q-badge color="red" floating>{{ product.discount }} Flash Sale</q-badge>
              </q-img>
              <q-card-section>
                <div class="text-h6 text-center text-red">{{ product.name }}</div>
                <div class="text-subtitle1 text-center text-red">{{ product.price }}</div>
              </q-card-section>
              <q-card-actions align="center">
                <q-btn flat icon="shopping_cart" label="Add to Cart" color="primary" />
                <q-btn flat icon="delete" label="Delete" color="negative" @click="deleteProduct(product)" />
              </q-card-actions>
            </q-card>
          </transition-group>
        </div>
      </q-page>
    </q-page-container>

    <!-- Footer -->
    <q-footer class="bg-blue-8 text-white">
      <q-toolbar>
        <q-toolbar-title>&copy; Official Shopping-in Aja</q-toolbar-title>
      </q-toolbar>
    </q-footer>
  </q-layout>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const leftDrawerOpen = ref(false);
    const slide = ref(0);
    const carouselImages = [
    'https://i.pinimg.com/564x/47/5b/59/475b59c61a6efb3ec8ac0a57e43fd03b.jpg',
    'https://i.pinimg.com/564x/4c/a1/4a/4ca14a4c8160baaa52ef3b53f9c5440d.jpg',
    'https://i.pinimg.com/564x/68/85/82/688582239f503010ac22ec7eada9b86b.jpg',
    'https://i.pinimg.com/564x/41/b8/30/41b830d872136129f78ba95b20035890.jpg',
    'https://i.pinimg.com/736x/b7/88/9c/b7889c9f8f90b5e6c968345a1148cd43.jpg'
    ];
    const products = ref([
      {
        name: 'Microwave',
        price: 'Rp. 1.200.000',
        image: 'https://i.pinimg.com/564x/4c/a1/4a/4ca14a4c8160baaa52ef3b53f9c5440d.jpg',
        discount: '10%'
      },
      {
        name: 'Kulkas 2 Pintu',
        price: 'Rp. 2.500.000',
        image: 'https://i.pinimg.com/564x/68/85/82/688582239f503010ac22ec7eada9b86b.jpg',
        discount: '15%'
      },
      {
        name: 'Kipas Angin',
        price: 'Rp. 499K',
        image: 'https://i.pinimg.com/564x/41/b8/30/41b830d872136129f78ba95b20035890.jpg',
        discount: '20%'
      },
      {
        name: 'Lampu',
        price: 'Rp. 350K',
        image: 'https://i.pinimg.com/736x/b7/88/9c/b7889c9f8f90b5e6c968345a1148cd43.jpg',
        discount: '25%'
      }
    ]);

    const deleteProduct = (product) => {
      products.value = products.value.filter(p => p.name !== product.name);
    };

    return {
      leftDrawerOpen,
      slide,
      carouselImages,
      products,
      deleteProduct
    };
  }
};
</script>

<style>
.carousel-slide img {
  width: auto;
  height: 40%; /* Menyesuaikan dengan kebutuhan */
  object-fit: contain;
  margin: auto;
}
.my-card {
  width: 100%;
  max-width: 500px;
  margin: 0 auto;
  border-radius: 10px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  transition: transform 0.2s, box-shadow 0.2s;
}
.my-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.2);
}
.my-card-img {
  border-radius: 10px 10px 0 0;
  height: 200px;
}
.q-footer {
  border-top: 1px solid #003285;
}
.text-red {
  color: red;
}
.fade-enter-active, .fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter, .fade-leave-to {
  opacity: 0;
}
</style>
