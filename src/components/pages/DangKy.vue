<template>
    <div class="container ts">
        <div class="formdk">
            <h1 class="text-center">ĐĂNG KÝ TÀI KHOẢN</h1>
            <P class="text-center">Bạn đã có tài khoản ? Đăng nhập <a href="#" @click.prevent="goToProducts">tại đây</a></P>
            <h2 class="text-center">THÔNG TIN CÁ NHÂN</h2>
            <div>
                <label for="">Họ *</label>
                <input type="text" class="form-control" v-model="ho" placeholder="Họ">
                <label for="">Tên *</label>
                <input type="text" class="form-control" v-model="ten" placeholder="Tên">
                <label for="">Số điện thoại *</label>
                <input type="text" class="form-control" v-model="sdt" placeholder="Số điện thoại">
                <label for="">Email *</label>
                <input type="text" class="form-control" v-model="email" placeholder="Email">
                <label for="">Mật khẩu *</label>
                <input type="text" class="form-control" v-model="mk" placeholder="Mật khẩu">
            </div>
            <button class="btn mt-3" @click="DKTC" >Đăng ký</button>
        </div>
    </div>
</template>
<script>
export default{
    data(){
        return{
            ho: '',
            ten: '',
            sdt: '',
            email: '',
            mk: '',
            tk:'',
        }
    },
    methods:{
        DKTC(){
            if(!this.ho||!this.ten||!this.sdt||!this.email||!this.mk){
                alert('Vui lòng nhập đủ thông tin!')
            }else{
                    alert('Bạn đã đăng ký thành công!')
            }
        },
        goToProducts() {
            this.$emit('changePage', 'DangNhap');
        },        
    }
}
</script>
<style>
.ts{
    display: flex;
   justify-content: center;
    align-items: center; 
}
.formdk{
    justify-content: center;
    align-items: center;
    width: 500px;
    max-width: 500px;
    min-width: 400px;
    margin-top: 20px;
    border: 1px solid black;
    border-radius: 10px;
    padding: 20px;
}
.formdk button{
    background-color: rgb(50, 205, 108);
    color: #fff;
    width: 100%;
}
.formdk button:hover{
    color: black;
}
</style>