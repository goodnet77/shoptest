      { id: 1, name: '티셔츠', category: '의류', price: 20000, image: 'https://shopby-images.cdn-nhncommerce.com/20250311/130455.710194000/250311_%EB%B3%80%EC%82%B0%EC%B2%9C%EC%95%88-%EB%A6%AC%EC%82%AC%EC%9D%B4%EC%A7%95_720.jpg?540x240' },
      { id: 2, name: '청바지', category: '의류', price: 40000, image: 'https://shopby-images.cdn-nhncommerce.com/20250313/155159.964965000/%EA%B0%80%EB%A1%9C%ED%98%95%20%EB%B0%B0%EB%84%88.jpg?540x240' },
      { id: 3, name: '스마트폰', category: '전자제품', price: 800000, image: 'https://shopby-images.cdn-nhncommerce.com/20250311/130455.710194000/250311_%EB%B3%80%EC%82%B0%EC%B2%9C%EC%95%88-%EB%A6%AC%EC%82%AC%EC%9D%B4%EC%A7%95_720.jpg?540x240' },
      { id: 4, name: '노트북', category: '전자제품', price: 1500000, image: 'https://shopby-images.cdn-nhncommerce.com/20250313/155159.964965000/%EA%B0%80%EB%A1%9C%ED%98%95%20%EB%B0%B0%EB%84%88.jpg?540x240' }
      
      // App.vue
      <template>
        <div class="container">
          <h1 class="title">Vue 쇼핑몰</h1>
          <div class="tabs">
            <button v-for="tab in tabs" :key="tab" @click="activeTab = tab" 
              :class="['tab-button', { active: activeTab === tab }]">
              {{ tab }}
            </button>
          </div>
          <div class="product-grid">
            <div v-for="product in filteredProducts" :key="product.id" class="product-card">
              <img :src="product.image" alt="상품 이미지" class="product-image">
              <h2 class="product-name">{{ product.name }}</h2>
              <p class="product-price">{{ product.price }}원</p>
            </div>
          </div>
        </div>
      </template>
      
      <script>
      import { ref, computed } from 'vue';
      
      export default {
        setup() {
          const tabs = ['전체', '의류', '전자제품'];
          const activeTab = ref('전체');
          const products = ref([
          { id: 1, name: '티셔츠', category: '의류', price: 20000, image: 'https://shopby-images.cdn-nhncommerce.com/20250311/130455.710194000/250311_%EB%B3%80%EC%82%B0%EC%B2%9C%EC%95%88-%EB%A6%AC%EC%82%AC%EC%9D%B4%EC%A7%95_720.jpg?540x240' },
      { id: 2, name: '청바지', category: '의류', price: 40000, image: 'https://shopby-images.cdn-nhncommerce.com/20250313/155159.964965000/%EA%B0%80%EB%A1%9C%ED%98%95%20%EB%B0%B0%EB%84%88.jpg?540x240' },
      { id: 3, name: '스마트폰', category: '전자제품', price: 800000, image: 'https://shopby-images.cdn-nhncommerce.com/20250311/130455.710194000/250311_%EB%B3%80%EC%82%B0%EC%B2%9C%EC%95%88-%EB%A6%AC%EC%82%AC%EC%9D%B4%EC%A7%95_720.jpg?540x240' },
      { id: 4, name: '노트북', category: '전자제품', price: 1500000, image: 'https://shopby-images.cdn-nhncommerce.com/20250313/155159.964965000/%EA%B0%80%EB%A1%9C%ED%98%95%20%EB%B0%B0%EB%84%88.jpg?540x240' }
   
          ]);
          const filteredProducts = computed(() => {
            return activeTab.value === '전체' ? products.value : products.value.filter(p => p.category === activeTab.value);
          });
      
          return { tabs, activeTab, filteredProducts };
        }
      };
      </script>
      
      <style>
      .container {
        padding: 20px;
        max-width: 1400px;
        margin: auto;
        font-family: Arial, sans-serif;
        background-color: #f8f9fa;
        border-radius: 8px;
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
      }
      .title {
        font-size: 32px;
        font-weight: bold;
        margin-bottom: 20px;
        text-align: center;
      }
      .tabs {
        display: flex;
        justify-content: center;
        gap: 20px;
        margin-bottom: 20px;
      }
      .tab-button {
        padding: 12px 24px;
        border-radius: 5px;
        cursor: pointer;
        background-color: transparent;
        color: #333;
        font-weight: bold;
        font-size: 20px;
        transition: color 0.3s;
        border: none;
      }
      .tab-button.active {
        font-weight: bold;
        color: #000;
      }
      .product-grid {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(400px, 1fr));
        gap: 30px;
      }
      .product-card {
        display: flex;
        flex-direction: column;
        align-items: center;
        border: 1px solid #ddd;
        padding: 25px;
        border-radius: 12px;
        background-color: white;
        text-align: center;
        transition: transform 0.2s, box-shadow 0.2s;
      }
      .product-card:hover {
        transform: translateY(-5px);
        box-shadow: 0 8px 16px rgba(0, 0, 0, 0.15);
      }
      .product-image {
        width: 100%;
        max-width: 700px;
        height: auto;
        object-fit: cover;
        border-radius: 12px;
      }
      .product-name {
        font-size: 22px;
        font-weight: bold;
        margin: 12px 0 6px;
      }
      .product-price {
        color: gray;
        font-size: 18px;
        margin: 0;
      }
      @media (max-width: 768px) {
        .container {
          max-width: 100%;
        }
        .product-grid {
          grid-template-columns: repeat(auto-fit, minmax(160px, 1fr));
        }
        .product-image {
          max-width: 300px;
        }
      }
      </style>