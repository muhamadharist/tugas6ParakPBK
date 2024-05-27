<template>
  <q-layout view="hHh lpR fFf">
    <!-- Header -->
    <q-header elevated class="bg-dark text-white" height-hint="98">
      <q-toolbar>
        <q-toolbar-title>
          <q-avatar>
            <img src="https://th.bing.com/th/id/OIP.DN6RSTWL_DNiL4yHYwayfAHaIg?rs=1&pid=ImgDetMain" alt="UIR STORE">
          </q-avatar>
          <span class="text-h6 q-ml-sm">UIR STORE</span>
        </q-toolbar-title>
        <q-btn dense round flat icon="shopping_cart" @click="toggleCartDrawer" class="text-white" />
      </q-toolbar>

      <!-- Tab Kategori -->
      <q-tabs align="left" class="bg-dark text-white">
        <q-tab label="Sport" />
        <q-tab label="Adventure" />
        <q-tab label="Matic" />
        <q-tab label="Cub" />
      </q-tabs>
    </q-header>

    <!-- Carousel -->
    <q-page-container>
      <q-carousel
        v-model="slide"
        swipeable
        animated
        infinite
        class="bg-grey-9"
        height="400px"
      >
        <q-carousel-slide
          v-for="(slide, index) in slides"
          :key="index"
          :name="index"
          :img-src="slide.img"
        >
          <div class="absolute-bottom text-center text-white q-pa-md overlay-text">
            <h4>M HARIST SAMUDRA DILILLA</h4>
          </div>
        </q-carousel-slide>
      </q-carousel>

      <!-- Product Cards -->
      <div class="row q-pa-md">
        <div class="card-list">
          <q-card 
            v-for="product in products" 
            :key="product.id" 
            class="q-mb-md product-card"
          >
            <q-img :src="product.img" :alt="product.name" />
            <q-card-section>
              <q-card-title>{{ product.name }}</q-card-title>
              <q-card-subtitle>{{ product.price }}</q-card-subtitle>
              <q-rating size="20px" value="4" readonly class="q-mb-sm" />
              <div class="row justify-between">
                <q-btn outline color="primary" label="Tambah ke Keranjang" @click="addToCart(product)" />
                <q-btn flat color="negative" label="Hapus" @click="removeFromCart(product)" />
              </div>
            </q-card-section>
          </q-card>
        </div>
      </div>
    </q-page-container>

    <!-- Keranjang Drawer -->
    <q-drawer
      v-model="cartDrawer"
      side="right"
      width="300"
      bordered
      class="bg-grey-10 text-white"
    >
      <q-list>
        <q-item-label header class="text-white">Keranjang</q-item-label>
        <q-item v-for="item in cart" :key="item.id" class="text-white">
          <q-item-section avatar>
            <q-img :src="item.img" :alt="item.name" />
          </q-item-section>
          <q-item-section>
            <q-item-label>{{ item.name }}</q-item-label>
            <q-item-label caption>{{ item.price }}</q-item-label>
          </q-item-section>
          <q-item-section side>
            <q-btn dense flat icon="remove_circle" @click="removeFromCart(item)" class="text-negative" />
          </q-item-section>
        </q-item>
      </q-list>
    </q-drawer>
  </q-layout>
</template>

<script>
export default {
  data() {
    return {
      slide: 0,
      cartDrawer: false,
      slides: [
        { img: 'https://via.placeholder.com/1920x400?text=Sport' },
        { img: 'https://via.placeholder.com/1920x400?text=Adventure' },
        { img: 'https://via.placeholder.com/1920x400?text=Matic' },
      ],
      products: [
        {
          id: 1,
          name: 'Honda CBR150R',
          price: 'Rp 35.000.000',
          img: 'https://th.bing.com/th/id/OIP.hgYmYdPBFT98GagY-A8L1QHaGH?rs=1&pid=ImgDetMain',
        },
        {
          id: 2,
          name: 'Yamaha MT-15',
          price: 'Rp 34.000.000',
          img: 'https://th.bing.com/th/id/OIP.YBeuOYvrAnIc1__YIcy1ygHaFj?rs=1&pid=ImgDetMain',
        },
        {
          id: 3,
          name: 'Kawasaki Ninja 250SL',
          price: 'Rp 43.000.000',
          img: 'https://th.bing.com/th/id/OIP.Kop5p19SBlRsFhxG_9ey-gAAAA?rs=1&pid=ImgDetMain',
        },
        {
          id: 4,
          name: 'Honda CBR 1000RR',
          price: 'Rp 800.000.000',
          img: 'https://th.bing.com/th/id/OIP.ILVF-jz-UjBuIYrznJ-wGQHaE8?rs=1&pid=ImgDetMain',
        },
        {
          id: 5,
          name: 'Yamaha R1 M',
          price: 'Rp 250.000.000',
          img: 'https://th.bing.com/th/id/OIP.k-YGsezs6l01IMLMFOSxJgHaE8?rs=1&pid=ImgDetMain',
        },
        {
          id: 6,
          name: 'Kawasaki ZX-25',
          price: 'Rp 99.000.000',
          img: 'https://th.bing.com/th/id/OIP.M66QAwEO7GOG_fQIdjNFrgHaFj?rs=1&pid=ImgDetMain',
        },
      ],
      cart: []
    }
  },
  methods: {
    addToCart(product) {
      this.cart.push(product);
      this.$q.notify({
        type: 'positive',
        message: `${product.name} ditambahkan ke keranjang`
      });
    },
    removeFromCart(product) {
      const index = this.cart.findIndex(p => p.id === product.id);
      if (index !== -1) {
        this.cart.splice(index, 1);
        this.$q.notify({
          type: 'negative',
          message: `${product.name} dihapus dari keranjang`
        });
      }
    },
    toggleCartDrawer() {
      this.cartDrawer = !this.cartDrawer;
    },
    checkImages() {
      this.products.forEach(product => {
        const img = new Image();
        img.src = product.img;
        img.onload = () => console.log(`${product.name} image loaded successfully`);
        img.onerror = () => console.error(`Error loading image for ${product.name}`);
      });
    }
  },
  mounted() {
    this.checkImages();
  }
}
</script>

<style>
body {
  background-color: #1e1e1e;
  color: #ffffff;
}

.row {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.q-pa-md {
  padding: 16px;
}

.card-list {
  display: flex;
  flex-wrap: wrap;
  gap: 16px;
  justify-content: center;
}

.product-card {
  background-color: #2c2c2c;
  color: #ffffff;
  width: calc(33% - 16px);
  min-width: 250px;
  transition: transform 0.3s, box-shadow 0.3s;
}

.product-card:hover {
  transform: translateY(-10px);
  box-shadow: 0 12px 20px rgba(0, 0, 0, 0.6);
}

.overlay-text {
  background-color: rgba(0, 0, 0, 0.7);
  padding: 10px;
}

.q-header, .q-tabs, .q-drawer {
  background-color: #333;
  color: #ffffff;
}

.q-btn {
  color: #ffffff;
}
</style>
