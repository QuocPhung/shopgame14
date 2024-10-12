<template>
    <div id="products" v-if="currentPage === 'products'">
        <div class="slideshow-container">
            <div class="slide" v-for="(image, index) in images" :key="index" v-show="currentSlide === index">
            <img :src="require(`@/assets/pic/${image}`)" alt="Slideshow image" />
            </div>
        
            <!-- Next and previous buttons -->
            <a class="prev" @click="prevSlide">&#10094;</a>
            <a class="next" @click="nextSlide">&#10095;</a>
        
            <!-- Dots/bullets -->
            <div class="dots">
            <span v-for="(image, index) in images" :key="index" class="dot" :class="{ active: currentSlide === index }" @click="goToSlide(index)"></span>
            </div>
        </div>

        <div class="container products my-3">
            <div class="tieude">
                <h1>Một Số Game Hot</h1>
                <a href="#" @click.prevent="goToProducts">Xem thêm</a>
            </div>
            <div class="product-items">
                <div class="product-item" v-for="product in products" :key="product.id">
                  <img :src="require(`@/assets/pic/${product.thum}`)" alt="">
                    <div class="product-item-text">
                        <h4>{{ product.name }}</h4>
                        <p><span>{{ product.price }}</span><sup>đ</sup></p>
                    </div>
                    <button @click="$emit('addToCart', product)">Thêm vào giỏ hàng</button>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
export default{
    name:'TrangChu',
    props:['product'],
    data(){
        return{
            currentPage: 'products',
            currentSlide: 0,
            products:[
                { id: 1, thum: "Back4blood.jpg", name: "Back 4 Blood", price: "1.464.144" },
                { id: 2, thum: "COD CW.jpg", name: "Call Of Duty (CW)", price: "1.464.144"},
                { id: 3, thum: "COD.jpg", name: "Call Of Duty", price: "496.651"},
                { id: 4, thum: "Diablo.jpg", name: "Diablo", price: "1.646.000",category:"kinhdi" },
                { id: 5, thum: "FF23.jpg", name: "Fifa 23", price: "1.590.000",category:"chienthuat" },
                { id: 6, thum: "Horizon.jpg", name: "Horizon Forbidden West", price: "1.999.000"},
                { id: 7, thum: "review-ghost-of-tsushima-directors-cut-gameplay-hadoan-tv-1.jpg", name: "Ghost Of Tsushima", price: "1.280.000"},
                { id: 8, thum: "GOW.jpg", name: "God Of War", price: "1.242.000"},
                { id: 9, thum: "GOWR.jpg", name: "God Of War Ragnarok", price: "1.400.000"},
                { id: 10, thum: "GTAV.jpg", name: "Grand Theft Auto V", price: "455.500"},
            ],
            images: [
                'Back4blood.jpg',
                'GTAV.jpg',
                'RDR.jpg',
                'BMW2.jpg'
            ],
        }
    },
    methods:{
        nextSlide() {
            this.currentSlide = (this.currentSlide + 1) % this.images.length;
        },
        prevSlide() {
            this.currentSlide = (this.currentSlide - 1 + this.images.length) % this.images.length;
        },
        goToSlide(index) {
            this.currentSlide = index;
        },
        goToProducts() {
            this.$emit('changePage', 'SanPham');
        },
        addToCart(shop) {
            this.$emit('addToCart', shop);
            alert(`${shop.name} đã được thêm vào giỏ hàng!`);
        }
    },
    mounted() {
        setInterval(() => {
        this.nextSlide();
    }, 3000);
    }
}
</script>
<style>
.products{
    border: 1px solid #EFF0F3;
    border-radius: 5px;
}
.tieude{
    display: flex;
    justify-content: space-between;
    align-items: center;
}
.tieude h1{
    color: #FF5622;
}
.tieude a{
    color: black;
    text-decoration: none;
    font-weight: 500;
}
.tieude a:hover{
    color: #FF5622;
}
.product-items {
    display: flex;
    justify-content: space-between;
    padding: 12px;
    flex-wrap: wrap;
}
.product-item {
    width: 19%;
    min-width: 200px;
    background-color: #fff;
    box-shadow: 0px 5px 10px gray;
    padding: 12px;
    margin-bottom: 12px;
    text-align: center;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
}
.product-item:hover {
    box-shadow: 0px 5px 10px rgba(0,0,0,0.2);
    transform: scale(1.05);
    transform: translateY(-5px);
}
.product-item img {
    border: 1px solid #2f2f2f;
    width: 100%;
    height: 50%;
    margin-bottom: 20px;
} 
.product-item-text h4 {
    font-size: 1rem;
}
.product-item button {
    margin-bottom: 12px;
    height: 30px;
    padding: 0 12px;
    cursor: pointer;
    border: none;
    border-radius: 5px;
}
.product-item button:hover {
    background-color: greenyellow;
    transform: translateY(-5px);
    box-shadow: 0px 5px 10px gray;
}
.btn-added {
    background-color: gray;
    color: white;
    border: none;
    cursor: not-allowed;
}
.slideshow-container {
  position: relative;
  max-width: 1000px;
  margin: auto;
  overflow: hidden;
}

.slide {
  display: flex;
  width: 100%;
  height: auto;
}

.slide img {
  width: 100%;
  height: auto;
}

.active {
  display: block;
}

.prev, .next {
  cursor: pointer;
  position: absolute;
  top: 50%;
  width: auto;
  margin-top: -22px;
  padding: 16px;
  color: white;
  font-weight: bold;
  font-size: 18px;
  transition: 0.6s ease;
  border-radius: 0 3px 3px 0;
  user-select: none;
  text-decoration: none;
}

.next {
  right: 0;
  border-radius: 3px 0 0 3px;
}

.prev:hover, .next:hover {
  background-color: rgba(0,0,0,0.8);
}

.dots {
  text-align: center;
  position: absolute;
  bottom: 15px;
  width: 100%;
}

.dot {
  cursor: pointer;
  height: 15px;
  width: 15px;
  margin: 0 2px;
  background-color: #bbb;
  border-radius: 50%;
  display: inline-block;
  transition: background-color 0.6s ease;
}

.active, .dot:hover {
  background-color: #717171;
}
</style>