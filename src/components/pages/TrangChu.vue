<template>
    <div id="products" v-if="currentPage === 'products'">
        <div class="slideshow-container">
            <div class="slide" v-for="(image, index) in images" :key="index" v-show="currentSlide === index">
            <img :src="require(`@/assets/pic/${image}`)" style="border-radius: 20px;margin-top: 10px;" alt="Slideshow image" />
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
                <div class="product-item" v-for="product in products" @click="showProductDetails(product)" :key="product.id">
                  <img :src="require(`@/assets/pic/${product.thum}`)" alt="">
                    <div class="product-item-text">
                        <h4>{{ product.name }}</h4>
                        <p><span>{{ product.price }}</span><sup>đ</sup></p>
                    </div>
                    <button @click.stop="$emit('addToCart', product)">Thêm vào giỏ hàng</button>
                </div>
            </div>
        </div>

        <div v-if="selectedProduct" class="product-modal">
            <div class="modal-content">
                <h3>Thông tin sản phẩm</h3>
                <img :src="getImageSrc(selectedProduct.thum)" alt="">
                <h4>{{ selectedProduct.name }}</h4>
                <p><span style="font-weight: bold;">Giá:</span> {{ formatPrice(selectedProduct.price) }} đ</p>
                <p><span style="font-weight: bold;">Mô tả:</span> {{ selectedProduct.description }}</p>
                <button class="btn" style="background-color: rgb(50, 205, 108);color: #fff;" @click="closeProductDetails">Đóng</button>
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
            selectedProduct: null,
            currentSlide: 0,
            products:[
                { id: 1, thum: "Back4blood.jpg", name: "Back 4 Blood", price: "1.464.144", description: "Back 4 Blood là một trò chơi bắn súng góc nhìn thứ nhất hợp tác đầy hồi hộp, được phát triển bởi những người sáng tạo ra thương hiệu Left 4 Dead nổi tiếng. Trò chơi đưa người chơi vào giữa cuộc chiến chống lại những sinh vật đáng sợ trong một thế giới khải huyền."  },
                { id: 2, thum: "COD CW.jpg", name: "Call Of Duty (CW)", price: "1.464.144", description:"Call of Duty là một series trò chơi điện tử thuộc thể loại bắn súng góc nhìn thứ nhất, được phát hành bởi Activision. Series này bắt đầu từ năm 2003 và chủ yếu tập trung vào các trận chiến quân sự và tình huống chiến đấu, với nhiều phiên bản khác nhau được phát hành qua các năm."},
                { id: 3, thum: "COD.jpg", name: "Call Of Duty", price: "496.651", description:"Call of Duty là một series trò chơi điện tử thuộc thể loại bắn súng góc nhìn thứ nhất, được phát hành bởi Activision. Series này bắt đầu từ năm 2003 và chủ yếu tập trung vào các trận chiến quân sự và tình huống chiến đấu, với nhiều phiên bản khác nhau được phát hành qua các năm."},
                { id: 4, thum: "Diablo.jpg", name: "Diablo", price: "1.646.000",category:"kinhdi", description:"Diablo là một series trò chơi điện tử hành động nhập vai về chủ đề dungeon crawler, được phát triển bởi Blizzard North và tiếp tục bởi Blizzard Entertainment. Series này nổi tiếng với gameplay hấp dẫn và cốt truyện tối tăm xoay quanh cuộc chiến giữa cái thiện và cái ác, với nhiều phần khác nhau, trong đó Diablo IV là phần thứ tư với nhân vật chính là Lilith, con gái của Mephisto." },
                { id: 5, thum: "FF23.jpg", name: "Fifa 23", price: "1.590.000",category:"chienthuat", description:"FIFA 23 mang đến trải nghiệm chân thật với hơn 19,000 cầu thủ, 700 đội bóng, 100 sân vận động và hơn 30 giải đấu. Người chơi có thể tham gia vào các giải đấu lớn nhất trên thế giới trong một trò chơi bóng đá đa dạng và phong phú." },
                { id: 6, thum: "Horizon.jpg", name: "Horizon Forbidden West", price: "1.999.000", description:"Horizon Forbidden West là một trò chơi điện tử nhập vai hành động thế giới mở được phát triển bởi Guerrilla Games và phát hành bởi Sony Interactive Entertainment vào năm 2022. Trò chơi đưa người chơi đến một tương lai xa, trong một thế giới hậu khải huyền, nơi bạn sẽ khám phá những vùng đất xa lạ, chiến đấu với những cỗ máy khổng lồ và gặp gỡ các bộ tộc mới đáng kinh ngạc."},
                { id: 7, thum: "review-ghost-of-tsushima-directors-cut-gameplay-hadoan-tv-1.jpg", name: "Ghost Of Tsushima", price: "1.280.000", description:"Ghost of Tsushima là một trò chơi hành động phiêu lưu thế giới mở, được phát triển bởi Sucker Punch Productions và phát hành bởi Sony Interactive Entertainment. Trò chơi có cốt truyện sâu sắc và ngoài các yếu tố chiến đấu, còn kết hợp cả cách tiếp cận lén lút. Người chơi sẽ khám phá một thế giới rộng lớn, đẹp mắt và immersive, tham gia vào những câu chuyện phụ bao quanh cốt truyện chính."},
                { id: 8, thum: "GOW.jpg", name: "God Of War", price: "1.242.000", description:"God of War là một trò chơi điện tử hành động phiêu lưu phát triển bởi Santa Monica Studio và được phát hành bởi Sony Interactive Entertainment vào năm 2018. Trong trò chơi, người chơi điều khiển Kratos, một chiến binh Spartan, với bối cảnh diễn ra trong thế giới của các vị thần Bắc Âu và quái vật, sau khi đã rời bỏ cuộc sống báo thù với các vị thần của Olympus."},
                { id: 9, thum: "GOWR.jpg", name: "God Of War Ragnarok", price: "1.400.000", description:"God of War Ragnarök là phần cuối cùng trong thời kỳ Bắc Âu, xoay quanh nhân vật Kratos, Thần Chiến Tranh, cùng với con trai Atreus, khi họ đối mặt với nguy cơ đến từ Ragnarök. Game thuộc thể loại hành động phiêu lưu, cho phép người chơi điều khiển Kratos và Atreus trong một cuộc hành trình để ngăn chặn sự xuất hiện của Ragnarök. Game nổi bật với đồ họa tuyệt đẹp, quy mô ấn tượng và lối chơi chiến đấu mạnh mẽ, mang lại cảm giác hài lòng và vô cùng mãnh liệt."},
                { id: 10, thum: "GTAV.jpg", name: "Grand Theft Auto V", price: "455.500", description:"Grand Theft Auto V (GTA V) là một trò chơi điện tử hành động phiêu lưu được phát triển bởi Rockstar North và phát hành bởi Rockstar Games vào năm 2013. Đây là phần thứ mười lăm trong series Grand Theft Auto và là phần thứ năm trong vũ trụ HD. Trò chơi diễn ra trong một thế giới mở rộng lớn và người chơi có thể thực hiện nhiều nhiệm vụ khác nhau, tham gia vào các hoạt động tội phạm và khám phá môi trường đa dạng của thành phố Los Santos và các khu vực lân cận."},
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
        },
        showProductDetails(product) {
            this.selectedProduct = product; // Lưu sản phẩm được chọn để hiển thị
        },
        closeProductDetails() {
            this.selectedProduct = null; // Đóng modal chi tiết sản phẩm
        },
        getImageSrc(thum) {
            return require(`@/assets/pic/${thum}`);
        },
        formatPrice(price) {
            return price.replace(/\B(?=(\d{3})+(?!\d))/g, "."); // Định dạng giá với dấu chấm
        },
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
.product-modal {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;
}

.modal-content {
    background-color: #fff;
    padding: 20px;
    border-radius: 10px;
    width: 50%;
    max-width: 600px;
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
    animation: fadeIn 0.3s ease-out;
}

@keyframes fadeIn {
    from {
        opacity: 0;
        transform: scale(0.8);
    }
    to {
        opacity: 1;
        transform: scale(1);
    }
}
</style>