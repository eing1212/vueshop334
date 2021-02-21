<template>
  
      <b-container>

    

    <b-row>
    <b-col cols="md-0-12"  v-for="product in products" :key="product.id">
    <b-card
    :title= 'product.ชื่อ'
    :img-src= "require(`@/assets/pic${product.id}.jpeg`)"
    img-alt="Image"
    img-top
    tag="article"
    style="max-width: 20rem;"
    class="mb-5 mr-5 ml-2"
    >
    <b-card-text>
      ราคา : {{product.price}} บาท
    </b-card-text>
    <b-button v-if="!product.cart" @click="add(product)"  href="#" variant="primary">เพิ่มรายการสินค้า</b-button>
     <b-button v-if="product.cart" @click="add(product)" :disabled="product.cart" href="#" variant="warning">เพิ่มสินค้าเรียบร้อย </b-button>
  </b-card>
    </b-col>
  </b-row>

  <b-row>
    <b-col>
      <h3>สถานะคำสั่งซื้อ</h3>
    </b-col>
  </b-row>


  <b-row>
    <b-col>
     <b-table bordered  hover :items="cart" :fields="fields" dark>
       
      
          <template slot="คำสั่งซื้อ" slot-scope="data" >
       {{ data.index+1}}
      </template>
        <template slot="ราคา" slot-scope="data" >
       {{ data.item.price * data.item.quantity}}
      </template>
       <template slot="ลบ" slot-scope="data" >
        <b-button @click="remove(data.item.id)" variant="danger"  >
          x
        </b-button>
      </template>
      <template slot="จำนวน" slot-scope="data">
        <b-row>
          <b-col cols="5">
             <b-button :disabled="data.item.quantity <=1" variant="primary" @click="decrement(data.item.id)"  class="mr-2">
          -
             </b-button>
          </b-col>
          <b-col cols="2">
            <h4>{{data.item.quantity}}</h4>
          </b-col>
          <b-col cols="5">
              <b-button variant="primary" @click="increment(data.item.id)" class="mr-2">
            +
        </b-button>
          </b-col>
        </b-row>
       
        
      
      </template>

      <template slot="รูปภาพ" slot-scope="data">
          <b-img style="max-width: 5rem;" :src= "require(`@/assets/pic${data.item.id}.jpeg`)" fluid alt="Responsive image"></b-img>
       
      </template>
      
     </b-table>

    </b-col>
  </b-row>
  <b-row v-if="cart.length > 0">
     <b-col></b-col>
     <b-col></b-col>
     <b-col></b-col>
     <b-col></b-col>
     <b-col><h5>ยอดที่ต้องชำระ</h5></b-col>
     <b-col><h5> {{ total }}.00 บาท</h5></b-col>
  </b-row>
  <b-row v-if="cart.length > 0">
     <b-col>
       <b-button @click="clean" variant="info" block class="mr-2">
          ล้างทั้งหมด
        </b-button>
     </b-col>
    <b-col></b-col>
     <b-col cols="4"></b-col>
    
     <b-col>
        
     </b-col>
     <b-col>
        <b-button    @click="buy" variant="success" block class="mr-2">
          ชำระเงิน
        </b-button>
     </b-col>
  </b-row>
   <b-modal hide-header-close no-close-on-esc no-close-on-backdrop ref="modal-1" centered title="รายการสั่งซื้อของคุณสำเร็จ ">
     <template slot="modal-footer">
       <b-button class="mt-3" variant="info" block @click="clean">ปิด</b-button>

       
    </template>
    <p  class="my-4">รายการสินค้า:</p>
    <ul v-for="productFinal in ticket.products" :key="productFinal.id">
      <li >
       ชื่อ: {{ productFinal.ชื่อ}}
      </li>
       <li >
       จำนวนสินค้า: {{ productFinal.quantity }} ชิ้น
      </li>
       <li >
       ราคา: {{ productFinal.price }} บาท 
      </li>
       <li >
       รวม: {{ productFinal.price * productFinal.quantity }} บาท
      </li>
      <hr>
    </ul>
    <h2 class="my-4">ยอดที่ต้องชำระ: {{ticket.total}}.00 บาท</h2>
   
    
  </b-modal>
  
   
      </b-container>
</template>

<script>
export default {
  ชื่อ: 'Cart',
  props: {
    msg: String
  },
  data(){
    return {
      ticket:{
        products: null,
        total:0
      },
      counter: 0,
      products: [
    {
        id:1,
        img:'@/assets/pic1.jpeg',
        ชื่อ:'หมวกแฟชั่น จากเรื่อง Kimetsu no Yaiba ',
        price:580,
        cart:false,
        quantity:1
       
    },
    {
        id:2,
        img:'@/assets/pic2.jpeg',
        ชื่อ:'เสื้อคลุมฮับบิ จากเรื่อง Kimetsu no Yaiba',
        price:950,
        cart:false,
        quantity:1
    },
    {
        id:3,
        img:'@/assets/pic3.jpeg',
        ชื่อ:'Wristband จากเรื่อง Kimetsu no Yaiba ',
        price:380,
        cart:false,
        quantity:1
    },
    {
        id:4,
        img:'@/assets/pic4.jpeg',
        ชื่อ:'เข็มกลัด พร้อมจี้ จากเรื่อง Kimetsu no Yaiba',
        price:580,
        cart:false,
        quantity:1
    },
    {
        id:5,
        img:'@/assets/pic5.jpeg',
        ชื่อ:'ดาบเหล็กไร้คม จากเรื่อง Kimetsu no Yaiba',
        price:1890,
        cart:false,
        quantity:1
    },
    {
        id:6,
        img:'@/assets/pic6.jpeg',
        ชื่อ:'เคสมือถือจากเรื่องKimetsu no Yaiba',
        price:480,
        cart:false,
        quantity:1
    },
],
  cart:[],
  fields: ['คำสั่งซื้อ', 'ลบ', 'รูปภาพ','ชื่อ','จำนวน','ราคา']
    } // data return
  },
  methods: {
     add(product){
       this.products[product.id-1].cart=true
       this.cart.push(product)
       this.counter++
     },
     clean(){
       this.cart=[];
      
       for (const key in this.products) {
          this.products[key].cart=false
          this.products[key].quantity=1
       }
       this.$refs['modal-1'].hide()
     },
    remove(id) {
      for (let index = 0; index < this.products.length; index++) {
       if (this.products[index].id == id) {
            this.products[index].cart=false
       } 
    }
    for (let index = 0; index < this.cart.length; index++) {
       if (this.cart[index].id == id) {
            this.cart.splice(index,1);
       } 
    }
    
},
buy(){
  this.ticket={
    products: this.cart,
    total: this.total
  }
  this.$refs['modal-1'].show()
  
}  ,
    increment(id){
      for (let index = 0; index < this.cart.length; index++) {
       if (this.cart[index].id == id) {
            this.cart[index].quantity++
       } 
    }
    },
    decrement(id){
      for (let index = 0; index < this.cart.length; index++) {
       if (this.cart[index].id == id) {
            this.cart[index].quantity--
       } 
    }
    }
  },
  computed: {
    total(){
      let t =0;
      for (let  index = 0; index < this.cart.length; index++) {
          t += this.cart[index].price*this.cart[index].quantity
      }
      return t
    }
  }
}
</script>

<style scoped>

</style>
