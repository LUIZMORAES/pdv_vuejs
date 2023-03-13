<template >
  <div class="logo-image" style="background-image: url('https://lcaminformatica.com.br/saas/assets/empresa/logo.png');">
  </div>

  <div class="home">

    <h2>
      Lista de produtos
    </h2>
    <h2>
      Escolha uma das opções abaixo:
    </h2>

    <div class="products">
      <div v-for="(product, index) in this.products" :key="index" class="product" :class="{ inBag: isInBag(product) }">
        <h4>{{ product.categoria }}</h4>
        <h4>{{ product.nome_produto }}</h4>
        <p class="price">R$ {{ product.preco_venda }}</p>
        <button v-if="!isInBag(product)" @click="addToBag(product)">Adicionar ao carrinho</button>
        <button v-else class="remove" @click="this.$store.dispatch('removeFromBag', product.id)">Remover do
          carrinho</button>
      </div>
    </div>
  </div>
</template>

<script>
import { mapState } from 'vuex'

export default {
  name: 'Home',
  data() {
    return {

    }
  },
  computed: mapState([
    'products',
    'productsInBag'
  ]),

  methods: {
    addToBag(product) {
      product.quantity = 1;
      this.$store.dispatch('addToBag', product);
    },
    isInBag(product) {
      return this.productsInBag.find(item => item.id == product.id)
    }
  }
}
</script>

<style lang="scss">
.logo-image {
  margin: auto;
  width: 350px;
  height: 70px;
  background-size: contain;
  background-position: center;
  background-repeat: no-repeat;

}

.home {
  background: #a855f7;

  .products {
    color: #fff;
    display: flex;
    flex-wrap: wrap;
    justify-content: center;


    .product {
      flex: 0 0 30%;
      box-sizing: border-box;
      box-shadow: 0 4px 8px 0 rgba(248, 246, 246, 0.2);
      padding: 16px;
      margin: 8px;
      height: 28 0px;

      @media only screen and (max-width: 769px) {
        flex: 0 0 40%;
      }

      @media only screen and (max-width: 640px) {
        flex: 0 0 90%;
      }

      &.inBag {
        border: 1px solid #007bff;
      }

      h4 {
        margin: 22px auto;
        font-size: 16px;
        max-width: 60%;
        font-weight: normal;
      }

      p.price {
        font-size: 20px;
        font-weight: bold;
      }

      button {
        color: #fff;
        background-color: #007bff;
        border: 1px solid #007bff;
        border-radius: 100px;
        font-weight: 400;
        text-align: center;
        padding: 8px 16px;
        cursor: pointer;

        &:hover {
          opacity: 0.8;
        }

        &.remove {
          background-color: transparent;
          border: none;
          color: black;
          text-decoration: underline;
        }
      }
    }
  }

}
</style>
