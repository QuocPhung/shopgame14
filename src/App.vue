<template>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.css" integrity="sha512-5A8nwdMOWrSz20fDsjczgUidUBR8liPYU+WymTZP1lmY9G6Oc7HlZv156XqnsgNUzTyMefFTcsFH/tnJE/+xBg==" crossorigin="anonymous" referrerpolicy="no-referrer" />
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-EVSTQN3/azprG1Anm3QDgpJLIm9Nao0Yz1ztcQTwFspd3yD65VohhpuuCOmLASjC" crossorigin="anonymous">
  <div id="app">
    <!--Header-->
    <div class="grid">      
            <nav class="header_nav">
                <ul class="header_nav-list">
                    <li class="header_nav-item"><a href="#" @click.prevent="changePage('TrangChu')"><img src="./assets/pic/logo.png" alt=""></a></li>
                    <li class="header_nav-item"><a href="#" @click.prevent="changePage('TrangChu')"><i class="fa fa-home" aria-hidden="true"></i> HOME</a></li>
                    <li class="header_nav-item"><a href="#" @click.prevent="changePage('SanPham')"><i class="fa fa-shopping-bag" aria-hidden="true"></i> SHOP</a></li>
                    <li class="header_nav-item"><a href="#"><i class="fa fa-newspaper-o" aria-hidden="true"></i> FORUMS</a></li>
                    <li class="header_nav-item"><a href="#"><i class="fa fa-windows" aria-hidden="true"></i> PHẦN MỀM</a>
                        <ul class="header_nav-submenu">
                            <li class="header_nav-item"><a href="#">Windows - Ghost</a></li>
                            <li class="header_nav-item"><a href="#">Office</a></li>
                            <li class="header_nav-item"><a href="#">Diệt Virut</a></li>
                            <li class="header_nav-item"><a href="#">Adobe</a></li>
                        </ul>
                    </li>
                    <li class="header_nav-item"><a href="#"><i class="fa fa-gamepad" aria-hidden="true"></i> GAME HOT</a></li>
                    <li class="header_nav-item"><a href="#"><i class="fa fa-weixin" aria-hidden="true"></i> BLOG</a></li>
                </ul>
                <ul class="header_nav-list">
                    <li class="header_nav-item"><a href="#" @click.prevent="changePage('GioHang')"><i class="fa fa-shopping-cart" aria-hidden="true"></i> GIỎ HÀNG ({{ cart.length }})</a></li>
                    <li class="header_nav-item"><button class="btn"><a href="#" @click.prevent="changePage('DangNhap')">Đăng Nhập</a></button></li>
                    <li class="header_nav-item header_nav-item--separate"><button class="btn"><a href="#" @click.prevent="changePage('DangKy')">Đăng Ký</a></button></li>
                </ul>
            </nav>
    </div>
    <!--Body-->
    <div>
      <trang-chu v-if="currentPage === 'TrangChu'" @changePage="changePage" @addToCart="addToCart" />
      <san-pham v-if="currentPage === 'SanPham'" @addToCart="addToCart" />
      <gio-hang v-if="currentPage === 'GioHang'" :cart="cart" @removeFromCart="removeFromCart" />
      <dang-nhap v-if="currentPage==='DangNhap'" @changePage="changePage" />
      <dang-ky v-if="currentPage==='DangKy'" @changePage="changePage" />
    </div>
    <!--Footer-->
    <div class="footer">
            <div class="lh container">
                <div class="col-sm-3">
                    <p>Địa chỉ: Tây Mỗ, Nam Từ Liêm, Hà Nội</p>
                    <p>SĐT: </p>
                    <p>Email: </p>
                </div>
                <div class="col-sm-3">
                    <ul>
                        <h5>CHÍNH SÁCH</h5>
                        <li><a href="#">Trang chủ</a></li>
                        <li><a href="#">Giới thiệu</a></li>
                        <li><a href="#">Sản phẩm</a></li>
                        <li><a href="#">Liên hệ</a></li>
                        <li><a href="#">Kiểm tra</a></li>
                    </ul>
                </div>
                <div class="col-sm-3">
                    <ul>
                        <h5>HỖ TRỢ KHÁCH HÀNG</h5>
                        <li><a href="#">Tìm kiếm</a></li>
                        <li><a href="#">Chính sách bảo mật</a></li>
                        <li><a href="#">Điều khoản dịch vụ</a></li>
                        <li><a href="#">Hưỡng dẫn kiểm tra đơn hàng</a></li>
                    </ul>
                </div>
                <div class="col-sm-3">
                    <ul>
                        <h5>LIÊN HỆ VỚI CHÚNG TÔI</h5>
                    </ul>
                </div>
            </div>
            <div class="bq">© Bản quyền thuộc về Quốc Huy</div>
    </div>    
  </div>
</template>
<script>
import TrangChu from './components/pages/TrangChu.vue';
import SanPham from './components/pages/SanPham.vue';
import GioHang from './components/pages/GioHang.vue';
import DangNhap from './components/pages/DangNhap.vue';
import DangKy from './components/pages/DangKy.vue';
export default{
  data(){
    return{
      currentPage: 'TrangChu',
      cart:[],
    }
  },
  components:{
    TrangChu,
    SanPham,
    GioHang,
    DangNhap,
    DangKy,
  },
  methods:{
    changePage(page) {
      this.currentPage = page;
    },
    addToCart(product) {
      // Thêm sản phẩm vào giỏ hàng
      this.cart.push(product);
      alert(`Đã thêm ${product.name} vào giỏ hàng!`);
    },
    removeFromCart(index) {
      this.cart.splice(index, 1); // Xóa sản phẩm khỏi giỏ hàng dựa trên chỉ mục
    }
  },
}
</script>
<style>
*{
    padding: 0;
    margin: 0;
    box-sizing: border-box;
}
.grid{
    width: 1200px;
    max-width: 100%;
    min-width: 200px;
    margin: 0 auto;
}
.header_nav{
    display: flex !important;
    justify-content: space-between !important;
    background-color: #1072BA;
    color: #fff;
    border-radius: 20px;
}
.header_nav-list{
    list-style-type: none;
    padding-left: 0px;
    margin-bottom: 0px;
}
.header_nav-item{
    display: inline-block;
    margin: 0 8px;
    position: relative;
    line-height: 60px;
}
.header_nav-item a{
    color: #fff;
    font-size: 1.2rem;
    text-decoration: none;
    font-weight: 400;
    height: auto;
}
.header_nav-item a:hover{
    color: #333;
}
.grid img{
    width: 40px;
    height: auto;
}
.header_nav-item button{
    background-color: rgb(50, 205, 108);
    line-height: 20px;
    padding: 5px;
    border: 1px solid rgb(50, 205, 108);
    border-radius: 10px;
}
.header_nav-item button:hover,
.product-item img:hover {
    transform: translateY(-2px);
    box-shadow: 0px 2px 5px black;
    background-color: rgb(50, 205, 108);
}
.header_nav-submenu{
    display: none;
    position: absolute;
    background-color: #fff;
    border: 1px solid black;
    top: 80%;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.3);
    z-index: 1;
}
.header_nav-submenu li{
    width: 150px;
}
.header_nav-list li:hover .header_nav-submenu{
    display: block;
}
.header_nav-submenu a{
    color: black;
}
.header_nav-submenu a:hover{
    color: #1072BA;
}
.footer{
    background-color: #1072BB;
    color: #fff;
    padding-top: 10px;
    margin-top: 10px;
}
.lh{
    display: flex;
    justify-content: center;
    
}
.lh ul{
    list-style-type: none;
}
.lh li a{
    color: #fff;
    text-decoration: none;
}
.bq{
    background-color: #222222;
    justify-content: center;
    text-align: center;
    padding: 10px;
}
</style>