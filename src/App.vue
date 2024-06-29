<template>
  <q-layout view="hHh lpR fFf">
    <!-- Navbar -->
    <q-header elevated class="bg-primary text-black">
      <q-toolbar>
        <q-btn dense flat round icon="menu" @click="toggleLeftDrawer" />
        <q-toolbar-title>
          Toko Ares
        </q-toolbar-title>
        <q-btn dense flat round icon="shopping_cart" @click="goToCart" />
      </q-toolbar>
    </q-header>

    <!-- Left Drawer -->
    <q-drawer v-model="leftDrawerOpen" side="left" width="100">
      <q-list>
        <q-item clickable v-ripple>
          <q-item-section>
            Home
          </q-item-section>
        </q-item>
        <q-item clickable v-ripple>
          <q-item-section>
            Products
          </q-item-section>
        </q-item>
        <q-item clickable v-ripple>
          <q-item-section>
            About Us
          </q-item-section>
        </q-item>
      </q-list>
    </q-drawer>

    <!-- Main Content -->
    <q-page-container>
      <q-page padding class="q-pa-md">
        <!-- Carousel -->
        <q-carousel
          v-model="slide"
          arrows
          infinite
          animated
          control-color="white"
          swipeable
          transition-prev="slide-right"
          transition-next="slide-left"
          height="500px"
          class="bg-dark text-black shadow-8 rounded-borders"
        >
          <q-carousel-slide v-for="(image, index) in carouselImages" :key="index" :name="index" :img-src="image">
          </q-carousel-slide>
        </q-carousel>

        <!-- Cards -->
        <div class="q-mt-xl row justify-center">
          <q-card v-for="(product, index) in products" :key="product.name" class="my-card q-mb-xl q-pa-md col-xs-12 col-sm-6 col-md-4 col-lg-3">
            <q-img :src="product.image" :alt="product.name" class="my-card-img">
            </q-img>
            <q-card-section>
              <div class="text-h5 text-center">{{ product.name }}</div>
              <div class="text-subtitle1 text-center">{{ product.price }}</div>
            </q-card-section>
            <q-card-actions align="center">
              <q-btn flat label="Add to Cart" color="primary" @click="addToCart(product)" />
              <q-btn flat label="Delete" color="negative" @click="deleteProduct(index)" />
            </q-card-actions>
          </q-card>
        </div>
      </q-page>
    </q-page-container>

    <!-- Footer -->
    <q-footer class="bg-white-1 text-black">
      <q-toolbar>
        <q-toolbar-title>
          &copy;Ares
        </q-toolbar-title>
        <div>
          <!---->
        </div>
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
      'https://api.rumahkapas.com/storage/uploads/2023/08/14/Jersey-Sepakbola_uid_64da1b044eb97.jpg',
      'https://1.bp.blogspot.com/-PZyYxzB5XDU/XpmkgWLE3UI/AAAAAAAAC5w/nmDxKHSUiEYTGOShLyuyhutbe75EWj3qgCLcBGAsYHQ/s1600/Toko%2BOnline%2BJual%2BJersey%2BBola.jpg'
    ];
    const products = ref([
  { 
    name: 'Kain Cotton Combed', 
    price: 'Rp. 105K/kg', 
    image: 'https://api.rumahkapas.com/storage/uploads/2023/03/04/IMG_3129_uid_6402d2e98e458.JPG'
  },
  { 
    name: 'Kain Cotton Carded', 
    price: 'Rp. 85K/kg', 
    image: 'https://api.rumahkapas.com/storage/uploads/2023/03/04/IMG_2935_uid_6402d32b5b8ee.JPG'
  },
  { 
    name: 'Kaos Polos Cotton Combed', 
    price: 'Rp. 35K', 
    image: 'https://api.rumahkapas.com/storage/uploads/2023/03/04/DSC01548_uid_6402d3d86937a.JPG', 
  },
  { 
    name: 'Kaos Motif Cotton Combed', 
    price: 'Rp. 25K', 
    image: 'https://api.rumahkapas.com/storage/uploads/2023/03/04/DSC01553_uid_6402d391117c5.JPG'
  }
]);

    const cart = ref([]);

    const toggleLeftDrawer = () => {
      leftDrawerOpen.value = !leftDrawerOpen.value;
    };

    const goToCart = () => {
      console.log('Navigating to cart...');
      // Logic untuk membuka halaman keranjang atau menampilkan keranjang
    };

    const addToCart = (product) => {
      cart.value.push(product);
      console.log(`${product.name} telah ditambahkan ke keranjang`);
    };

    const deleteProduct = (index) => {
      products.value.splice(index, 1);
      console.log(`Product at index ${index} has been deleted`);
    };

    return {
      leftDrawerOpen,
      toggleLeftDrawer,
      slide,
      carouselImages,
      products,
      addToCart,
      goToCart,
      deleteProduct
    };
  }
};
</script>

<style>
.my-card {
  width: 100%;
  max-width: 500px;
  margin: 0 auto;
  border-radius: 10px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

.my-card-img {
  border-radius: 10px 10px 0 0;
  height: 200px;
}

.rounded-borders {
  border-radius: 10px;
}

.q-footer {
  border-top: 1px solid #7a0085;
}
</style>
