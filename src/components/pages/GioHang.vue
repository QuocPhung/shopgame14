<template>
    <div class="container gh">
        <h1 class="text-center">Giỏ hàng</h1>
        <div class="container" v-if="cart && cart.length > 0" >
            <div class="empty">
                <div class="cart-item" v-for="(item, index) in cart" :key="index">
                    <img :src="getImageSrc(item.thum)" alt="">
                    <div class="cart-item-details">
                        <h4>{{ item.name }}</h4>
                        <p><span>{{ formatPrice(item.price) }}</span><sup>đ</sup></p>
                        <button class="btn xoa" @click="removeFromCart(index)">Xóa</button>
                    </div>
                </div>
                <div class="d-flex done">
                    <h3>Tổng tiền: {{ totalCartPrice() }} đ</h3>
                    <button class="btn">Thanh toán</button>
                </div>
            </div>
        </div>
        <div class="" v-else>
            <p>Giỏ hàng của bạn đang trống.</p>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        cart: Array,
    },
    name: 'GioHang',
    methods: {
        removeFromCart(index) {
            this.$emit('removeFromCart', index); // Phát sự kiện để xóa sản phẩm khỏi giỏ hàng
        },
        totalCartPrice() {
            return this.cart.reduce((total, item) => {
                const priceNumber = parseFloat(item.price.replace(/\./g, '').replace(/,/g, ''));

                return total + priceNumber;
            }, 0).toLocaleString();
        },
        getImageSrc(thum) {
            return require(`@/assets/pic/${thum}`);
        },
        formatPrice(price) {
            return price.replace(/\B(?=(\d{3})+(?!\d))/g, "."); // Định dạng giá với dấu chấm
        },
    },
}
</script>

<style>
.gh{
    margin: 10px 0px 10px 0px;
    border: 1px solid #EFF0F3;
    border-radius: 5px;
}
.cart-item {
    display: flex;
    margin: 10px 0px 10px 0px;
    padding: 10px;
    border: 1px solid #2f2f2f;
    border-radius: 5px;
}
.cart-item img {
    width: 350px;
    height: 200px;
    border: 1px solid #2f2f2f;
    border-radius: 5px;
    margin-right: 10px;
}
.cart-item-details {
    display: flex;
    flex-direction: column;
    justify-content: center;
}
.empty button{
    background-color: rgb(50, 205, 108);
    color: #FFF;
}
.empty button:hover{
    color: black;
}
.xoa{
    width: 100px;
}
.done{
    justify-content: space-between;
}
</style>
