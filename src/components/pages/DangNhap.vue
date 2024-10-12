<template>
    <div class="container ts">
        <div class="formdn">
            <h1>Đăng nhập</h1>
            <label for="">Tài khoản</label>
            <input type="text" class="form-control" v-model="tk" placeholder="Số điện thoại hoặc email">
            <label for="">Mật khẩu</label>
            <input type="text" class="form-control" v-model="mk" placeholder="Mật khẩu">
            <div class="row">
                <button class="btn mt-3" @click="DNTC">Đăng nhập</button>
                <button class="btn mt-3" @click.prevent="goToProducts">Đăng ký</button>
            </div>
        </div>
    </div>
</template>
<script>
export default{
    data(){
        return{
            mk: '',
            tk:'',
        }
    },
    methods:{
        DNTC(){
            if(!this.tk||!this.mk){
                alert('Vui lòng nhập đủ thông tin!')
            }else{
                alert('Bạn đã đăng nhập thành công')
                this.currentPage='products'
            }
        },
        goToProducts() {
            this.$emit('changePage', 'DangKy');
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
.formdn{
    
    width: 500px;
    max-width: 500px;
    margin-top: 20px;
    border: 1px solid black;
    border-radius: 10px;
    padding: 20px;
}
.formdn button{
    background-color: rgb(50, 205, 108);
    color: #fff;
    width: 100%;
}
.formdn button:hover{
    color: black;
}
</style>