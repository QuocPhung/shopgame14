<template>
    <div>
        <div class="container products my-3">
            <h1>Kho Game</h1>
            <div>
                <label for="category">Chọn thể loại:</label>
                <select class="pick" v-model="selectedCategory">
                    <option value="all">Tất cả</option>
                    <option value="hanhdong">Hành động</option>
                    <option value="sinhton">Sinh tồn</option>
                    <option value="bansung">Bắn súng</option>
                    <option value="nhapvai">Nhập vai</option>
                </select>
            </div>
            <div class="product-items">
                <div class="product-item" v-for="shop in filteredShops" :key="shop.id">
                    <img :src="require(`@/assets/pic/${shop.thum}`)" alt="">
                    <div class="product-item-text">
                        <h4>{{ shop.name }}</h4>
                        <p><span>{{ shop.price }}</span><sup>đ</sup></p>
                    </div>
                    <button @click="addToCart(shop)">Thêm vào giỏ hàng</button>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
    export default{
        name:'SanPham',
        props:['products'],
        data(){
            return{
                selectedCategory: 'all',
                shops:[    
                    { id: 1, thum: "Back4blood.jpg", name: "Back 4 Blood", price: "1.464.144",category:"sinhton" },
                    { id: 2, thum: "COD CW.jpg", name: "Call Of Duty (CW)", price: "1.464.144",category:"bansung"},
                    { id: 3, thum: "COD.jpg", name: "Call Of Duty", price: "496.651",category:"bansung"},
                    { id: 4, thum: "Diablo.jpg", name: "Diablo", price: "1.646.000",category:"kinhdi" },
                    { id: 5, thum: "FF23.jpg", name: "Fifa 23", price: "1.590.000",category:"chienthuat" },
                    { id: 6, thum: "Horizon.jpg", name: "Horizon Forbidden West", price: "1.999.000",category:"sinhton" },
                    { id: 7, thum: "review-ghost-of-tsushima-directors-cut-gameplay-hadoan-tv-1.jpg", name: "Ghost Of Tsushima", price: "1.280.000",category:"nhapvai" },
                    { id: 8, thum: "GOW.jpg", name: "God Of War", price: "1.242.000",category:"nhapvai" },
                    { id: 9, thum: "GOWR.jpg", name: "God Of War Ragnarok", price: "1.400.000",category:"nhapvai" },
                    { id: 10, thum: "GTAV.jpg", name: "Grand Theft Auto V", price: "455.500",category:["nhapvai","thegioimo"] },
                    { id: 11, thum: "FH5.jpg", name: "Forza Horizon 5", price: "382.344",category:"hanhdong" },
                    { id: 12, thum: "FFV.jpg", name: "Final Fantasy V", price: "399.000",category:"hanhdong" },
                    { id: 13, thum: "DB.jpg", name: "Dragon Ball", price: "680.000",category:"hanhdong" },
                    { id: 14, thum: "kdr.jpg", name: "Kingdom Rush 5", price: "446.647",category:"hanhdong" },
                    { id: 15, thum: "slh.jpg", name: "Silent Hill 2 Remake", price: "797.211",category:"hanhdong" },
                    { id: 16, thum: "re3.jpg", name: "Resident Evil 3", price: "520.000",category:"kinhdi" },
                    { id: 17, thum: "GT.jpg", name: "Ghostwire Tokyo", price: "749.000",category:"kinhdi" },
                    { id: 18, thum: "BR.jpg", name: "Backrooms: Last Room", price: "384.000",category:"kinhdi" },
                    { id: 19, thum: "re2.jpg", name: "Risident Evil 2", price: "920.521",category:"kinhdi" },
                    { id: 20, thum: "LC.jpg", name: "Lethal Company", price: "248.201",category:"kinhdi" },
                    { id: 21, thum: "Grouded.jpg", name: "Grounded", price: "148.211",category:"sinhton" },
                    { id: 22, thum: "GH.jpg", name: "Green Hell", price: " 68.276",category:"sinhton" },
                    { id: 23, thum: "SM.jpg", name: "Soulmark", price: "670.566",category:"sinhton" },
                    { id: 24, thum: "SV.jpg", name: "Stardew Valley", price: "84.208",category:"sinhton" },
                    { id: 25, thum: "Mine.jpg", name: "Minecraft", price: "1.163.000",category:"sinhton" },
                    { id: 26, thum: "BMW2.jpg", name: "Black Myth Wukong", price: "1.599.000",category:"nhapvai" },                   
                ]
            }
        },
        methods:{
            addToCart(shop) {
                this.$emit('addToCart', shop);
            }
        },
        computed:{
            filteredShops() {
                if (this.selectedCategory === 'all') {
                    return this.shops;
                }
                    return this.shops.filter(shop => shop.category === this.selectedCategory);
            }
        },
    }
</script>
<style>
.products{
    border: 1px solid #EFF0F3;
    border-radius: 5px;
}
h1{
    text-align: center;
    color: #FF5622;
}
.pick{
    margin: 5px;
    border-radius: 5px;
}
.product-items {
    display: flex;
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

</style>