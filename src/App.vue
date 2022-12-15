<template>
<div class="app">

  <div class="container">
    
    <nav class="nav justify-content-center">
      <a class="nav-link active" href="#" aria-current="page">Home</a>
      <a class="nav-link active" href="#" aria-current="page">Product</a>
      <a class="nav-link active" href="#" aria-current="page">Download App</a>
      <a class="nav-link active" href="#" aria-current="page">Git Hub Code</a>
      <a class="nav-link active" href="#" aria-current="page">About us</a>
    </nav>
    
    <div class="add-product">
      
        <label for="" class="form-label">Название товара:</label>
        <input type="text" class="form-control" id="name" aria-describedby="helpId" v-model.value="inputName">

        <label for="" class="form-label">Цена за единицу товара:</label>
        <input type="number" class="form-control" id="price" aria-describedby="helpId" v-model.value="inputPrice">
        
        <label for="" class="form-label">Количество товара:</label>
        <input type="number" class="form-control" id="quantity" aria-describedby="helpId" v-model.value="inputQuantity">

        <label for="" class="form-label">Дата приема товара:</label>
        <input type="date" class="form-control" id="dates" aria-describedby="helpId" min="01-01,2022" v-model.value="inputDate">


        <br>

        <div class="d-grid gap-2">
          <button type="button" class="btn btn-primary" @click="checkToEmpty">Добавить товар</button>
        </div>
      
    </div>
    

    <div class="total-price">
        <div class="alert alert-primary" role="alert">
          Общая сумма за товаров: <strong>{{totalPrice}}$</strong>
        </div>
    </div>

    <div class="products-list" v-for="(product, index) in products">
      <div class="product">
        <span>Порядковый номер: {{index + 1}}</span> <br>
        <span>Название: {{product.productName}}</span> <br>
        <span>Цена: {{product.price}}$ / за штук</span> <br>
        <span>Количество: {{product.quantity}}шт</span> <br>
        <span>Дата приема товара: {{product.date}}</span> <br>
        <span>Общая цена: {{product.price * product.quantity}}$</span> <br>
        <div class="remove">
            <button type="button" name="plus" class="btn btn-danger" @click="removeProduct(index)">Удалить</button>
        </div>
      </div>
    </div> 
  </div>
</div>




</template>

<script>


export default {
  data() {
    return {
      products: [
        {productName: "ГЕНЕРАТОР БЕНЗИНОВЫЙ TOR TR2500E 2 КВТ 220В", price: 1200, quantity:15,date:"12-04-2022"},
        {productName: "КИТАЙСКИЙ ОРИГИНАЛНЫЙ ПРОЦЕССОР Core Xeon Gold 6250", price: 1500, quantity:230,date:"12-04-2022"},
        {productName: "IPHONE SUPER ULTRA MAX 999TB MEGA PRO VERSION 99X", price: 1000, quantity:30,date:"12-04-2022"},
        {productName: "НОУТБУК SAMSUNG 2ЯДРА 3ГИГА ИГРОВАЯ ВИДЕОКАРТА", price: 2000, quantity:5,date:"12-04-2022"},
        {productName: "КИНДЕР СЮРПРИЗ", price: 100, quantity:20, date:"12-04-2022"},
        {productName: "НАРУЧНЫЕ ЧАСЫ ROLEX ОРИДЖИНАЛ 100ПРОЦ", price: 10, quantity:1,date:"12-04-2022"},
      ],
      inputName: "",
      inputPrice: "",
      inputQuantity: "",
      inputDate: "",
      totalPrice: 0
    }
  },
  methods: {
    onInput(e, product) {
      product.quantity = Math.max(0, parseInt(e.target.value) || 0);
  },
  addProduct () {
    this.products.unshift({
      productName:this.inputName,
      price:this.inputPrice,
      quantity:this.inputQuantity,
      date:this.inputDate
    }),
    this.inputName = "", this.inputPrice = "", this.inputQuantity = "", this.inputDate = "";
    this.priceResult ();
  },
  checkToEmpty () {
    if (this.inputName == "") {
      document.querySelector("#name").classList.add("empty");
      return
    }
    if (this.inputPrice == "" || this.inputPrice <= 0) {
      document.querySelector("#name").classList.remove("empty");
      document.querySelector("#price").classList.add("empty");
      return
    }
    if (this.inputQuantity == "" || this.inputQuantity <= 0) {
      document.querySelector("#name").classList.remove("empty");
      document.querySelector("#price").classList.remove("empty");
      document.querySelector("#quantity").classList.add("empty");
      return
    }
    if (this.inputDate == "") {
      document.querySelector("#name").classList.remove("empty");
      document.querySelector("#price").classList.remove("empty");
      document.querySelector("#dates").classList.add("empty");
      return
    }
    else 
      document.querySelector("#name").classList.remove("empty");
      document.querySelector("#price").classList.remove("empty");
      document.querySelector("#dates").classList.remove("empty");
      this.addProduct();
  },
  removeProduct (index) {
    this.products.splice(index, 1),
    this.priceResult ();
  },
  priceResult () {
    this.totalPrice = 0;
    for (let i in this.products) {
      let idx = i
      let itemPrice = this.products[idx].price
      let itemQuantity = this.products[idx].quantity
      this.totalPrice += itemPrice * itemQuantity 
    }
   },
  }, 
  mounted () {
    this.priceResult ()
   }
}
</script>
<style scoped>
  .product {
    margin: 20px 0;
    padding: 10px;
    border: 2px solid rgb(154, 232, 232);
    border-radius: 10px;
    background-color: rgb(228, 255, 255);
  }
  .empty {
    border-color: red;
  }

  .add-product label {
    padding-left: 10px;
  }
  
  .total-price {
    margin-top: 15px;
  }
  
</style>