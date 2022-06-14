<template>
  <div class="container">
    <!-- Header -->
    <header>
      <div class="head">
        <i class="bi bi-list"></i>
        <h1>Sneakers</h1>
        <nav>
          <ul>
            <li>Collections</li>
            <li>Men</li>
            <li>Women</li>
            <li>About</li>
            <li>Contact</li>
          </ul>
        </nav>
      </div>
      <div class="profile">
        <i class="bi bi-cart3"></i>
        <img src="@/assets/profile-picture.jpg" alt="Profile Image" class="profile-image">
      </div>
    </header>

    <div class="row">

      <div class="image">
        <img src="@/assets/image4.jpg" alt="Product Image" class="product-image">
        <i class="bi bi-chevron-left" @click="prev"></i>
        <i class="bi bi-chevron-right" @click="next"></i>
        <div class="images">
          <img v-for="image in images" :src="image.src" class="small-product-image" :id="image.id" :alt="image.alt" :key="image.id">
        </div>
      </div>

      <div class="text">
        <p class="title">SNEAKER COMPANY</p>
        <h1>Fall Limited Edition Sneakers</h1>
        <p class="about">These low-profile sneakers are your perfect casual wear companion. Featuring a durable rubber outer sole, they'll withstand everything the weather can offer.</p>
        <div class="price-row">
          <div>
            <p class="current-price">$125.00</p>
            <span class="discount">50%</span>
          </div>
          <p class="former-price">$250.00</p>
        </div>
        <div class="counter-row">
          <div class="counter">
            <p class="minus" @click="decrement">-</p>
            <p class="count">{{ count }}</p>
            <p class="plus" @click="increment">+</p>
          </div>
          <div class="button-div">
            <button><i class="bi bi-cart3"></i>Add to Cart</button>
          </div>
        </div>
      </div>

    </div>
  </div>
</template>

<script>
export default {
  name: 'ProductPage',
  data () {
    return {
      count: 0,
      images: [
        { id: 0, src: require('@/assets/image0.jpg'), alt: 'Product Image', class: 'small-product-image' },
        { id: 1, src: require('@/assets/image1.jpg'), alt: 'Product Image', class: 'small-product-image' },
        { id: 2, src: require('@/assets/image2.jpg'), alt: 'Product Image', class: 'small-product-image' },
        { id: 3, src: require('@/assets/image3.jpg'), alt: 'Product Image', class: 'small-product-image' }
      ],
      mobileImages: [
        { id: 0, src: require('@/assets/image0.jpg'), alt: 'Product Image' },
        { id: 1, src: require('@/assets/image1.jpg'), alt: 'Product Image' },
        { id: 2, src: require('@/assets/image2.jpg'), alt: 'Product Image' },
        { id: 3, src: require('@/assets/image3.jpg'), alt: 'Product Image' },
        { id: 4, src: require('@/assets/image4.jpg'), alt: 'Product Image' }
      ]
    }
  },
  methods: {
    increment () {
      this.count++
    },
    decrement () {
      if (this.count === 0) {
        this.count = 0
      } else {
        this.count--
      }
    },
    next () {
      let next
      const image = this.$el.querySelector('.product-image')
      const path = image.src
      const start = path.indexOf('image')
      const end = start + 5
      // console.log(image, path, start, end)
      const current = path.charAt(end)
      if (parseInt(current) === 4) {
        next = 0
      } else {
        next = parseInt(current) + 1
      }
      // console.log(current, next)
      image.src = this.mobileImages[next].src
    },
    prev () {
      let prev
      const image = this.$el.querySelector('.product-image')
      const path = image.src
      const start = path.indexOf('image')
      const end = start + 5
      const current = path.charAt(end)
      if (parseInt(current) === 0) {
        prev = 4
      } else {
        prev = parseInt(current) - 1
      }
      // console.log(current, prev)
      image.src = this.mobileImages[prev].src
    }
  },
  mounted () {
    this.$el.querySelectorAll('.small-product-image').forEach(el => {
      el.addEventListener('click', () => {
        this.$el.querySelector('.product-image').src = this.images[el.id].src
      })
    })
  }
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Poppins&display=swap');
/* @import url('https://fonts.googleapis.com/css2?family=Noto+Sans&display=swap'); */
@import url("https://cdn.jsdelivr.net/npm/bootstrap-icons@1.8.3/font/bootstrap-icons.css");

*{
  box-sizing: border-box;
  font-family: 'Poppins', sans-serif;
}

div.container{
  width: 100%;
  margin: 0 0 100px;
  padding: 0;
}

header{
  width: 100%;
  height: 10vh;
  margin: auto;
  padding: 10px 15px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.bi-list{
  margin-right: 20px;
  font-size: 2rem;
  font-weight: 900;
  color: #222;
}

h1{
  color: #1B1E25;
  font-weight: 900;
  font-size: 2.2rem;
  /* font-family: 'Noto Sans', sans-serif; */
}

nav{
  display: none;
}

.profile, .head{
  display: flex;
  justify-content: space-around;
  align-items: center;
}

.bi-cart3{
  margin-right: 25px;
  font-size: 1.8rem;
  font-weight: 900;
  color: #666;
}
.profile-image{
  width: 30px;
  height: 30px;
  border-radius: 50%;
}

div.row, div.counter-row{
  width: 100%;
  margin: 0;
  padding: 0;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: flex-start;
}

.image{
  width: 100%;
  position: relative;
}

.product-image{
  width: 100%;
  height: 400px;
}

.images{
  display: none;
}

.bi-chevron-left, .bi-chevron-right{
  padding: 9px 13px;
  color: #000;
  background: #FFF;
  border-radius: 50%;
  -webkit-text-stroke: 2px;
  font-size: 1.1rem;
  position: absolute;
  top: 45%;
  z-index: 5;
}

.bi-chevron-left{
  left: 15px;
}

.bi-chevron-right{
  right: 15px;
}

.text{
  width: 100%;
  padding: 10px 20px;
}

.title{
  color: #FF7D1B;
  font-weight: 600;
}

.text h1{
  font-weight: 900;
  color: #000;
}

.about{
  color: #828486;
  font-weight: 500;
}

.price-row{
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
}

.price-row div{
  display: flex;
  justify-content: safe;
  align-items: center;
}

.current-price{
  font-size: 2rem;
  font-weight: 900;
  color: #000;
}
.discount{
  margin-left: 20px;
  padding: 3px 9px;
  font-size: 0.9rem;
  font-weight: 600;
  color: #FF7D1B;
  background: #FCEADC;
  border-radius: 6px;
}

.former-price{
  color: #8D8E90;
  font-size: 1.1rem;
  font-weight: 600;
  text-decoration: line-through;
}

.counter{
  width: 100%;
  margin: 20px auto;
  padding: 20px 25px;
  background: #EEEFF7;
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-radius: 15px;
}

.counter p{
  margin: 0;
  font-size: 1.5rem;
  font-weight: 900;
  cursor: pointer;
}

.plus, .minus{
  color: #F87D20;
}

.button-div{
  width: 100%;
  margin: 20px auto;
}

button .bi-cart3{
  margin-right: 15px;
  font-size: 1.1rem;
  -webkit-text-stroke: .3px;
  color: #FFF;
}

button{
  width: 100%;
  padding: 20px 25px;
  color: #FFF;
  background: #F87D20;
  outline: none;
  border: none;
  border-radius: 15px;
  font-size: 1.1rem;
  font-weight: 600;
}

button:hover{
  box-shadow: #FCE7D8 0px 7px 25px 10px;
  transform: scale(1.01)
}

@media(max-width: 300px){
  h1, .bi-list, header .bi-cart3{
    font-size: 1.5rem;
  }

  .product-image{
    height: 350px;
  }

  .discount{
    font-size: 0.8rem;
    margin-right: 30px;
  }

  .current-price, .former-price{
    font-size: 1rem;
  }

  .counter, button{
    padding: 10px 15px;
  }
}
@media (min-width: 800px) {
  div.container{
    width: 85%;
    margin: auto;
  }

  div.row{
    width: 95%;
  }

  div.row, div.counter-row{
    flex-direction: row;
  }

  header{
    height: 15vh;
    padding: 10px 5px;
    margin-bottom: 60px;
    border-bottom: 1px solid #ccc;
  }

  .bi-list{
    display: none;
  }

  nav{
    display: block;
  }

  nav ul{
    display: flex;
    justify-content: space-between;
    align-items: center;
    list-style: none;
  }

  nav ul li{
    margin: 10px;
    padding: 5px;
    color: #95969B;
  }

  nav ul li:hover{
    transform: scale(1.1);
    cursor: pointer;
  }

  .bi-cart3{
    margin-right: 50px;
  }

  .profile-image{
    width: 45px;
    height: 45px;
  }

  .image{
    padding: 30px 60px;
  }

  .product-image{
    height: 450px;
    border-radius: 15px;
  }

  .bi-chevron-left, .bi-chevron-right{
    display: none;
  }

  .images{
    width: 100%;
    margin: 30px auto;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
  }

  .small-product-image{
    width: 20%;
    height: 90px;
    border-radius: 10px;
  }

  .small-product-image:hover{
    border: 2px solid #FF7D1B;
  }

  .text{
    padding: 60px 20px 30px 60px;
  }

  .text h1{
    font-size: 2.3rem;
  }

  .price-row{
    flex-direction: column;
    justify-content: space-between;
    align-items: flex-start;
  }

  .price-row div{
    margin-top: -20px;
  }

  .former-price{
    margin-top: -25px;
  }

  .counter{
    width: 40%;
    padding: 10px 15px;
  }

  .button-div{
    width: 54%;
  }

  button{
    padding: 15px 20px;
  }
}
</style>
