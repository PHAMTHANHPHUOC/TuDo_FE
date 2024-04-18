<template>
    <div class="row">
        <div class="col-lg-4">
            <div class="card">
                <div class="card-body">
                    <div class="d-flex flex-column align-items-center text-center">
                        <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTnO0uhwiK1yDASJ6SkO3SLFNU3dtIb4NMiBA&s"
                            alt="Quản trị viên" class="rounded-circle p-1 bg-primary" width="110">
                    </div>
                    <hr class="my-4">
                    <button  class="btn btn-outline-info ">Nạp Tiền</button>
                </div>
            </div>
        </div>
        <div  class="col-lg-8">
            <div class="card">
                <div class="card-body">
                    <div class="row mb-3">
                        <div class="col-sm-3">
                            <h6 class="mb-0">Họ Và Tên</h6>
                        </div>
                        <div class="col-sm-9 text-secondary">
                            <input v-model="profile.ho_va_ten" type="text" class="form-control" >
                        </div>
                    </div>
                    <div class="row mb-3">
                        <div class="col-sm-3">
                            <h6 class="mb-0">Email</h6>
                        </div>
                        <div class="col-sm-9 text-secondary">
                            <input v-model="list_khach_hang.email"  type="email" class="form-control" >
                        </div>
                    </div>
                    <div class="row mb-3">
                        <div class="col-sm-3">
                            <h6 class="mb-0">Số Điện Thoại</h6>
                        </div>
                        <div class="col-sm-9 text-secondary">
                            <input v-model="list_khach_hang.so_dien_thoai"  type="text" class="form-control" >
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import baseRequest from '../../../../core/baseRequest';
import axios from 'axios';
import { createToaster } from "@meforma/vue-toaster";
const toaster = createToaster({ position: "top-right" });
export default {
    data() {
        return {
            profile: {},
            update_password: {},
            create_thanh_toan:{},
            list_khach_hang:{},


        }
    },
    mounted() {
        this.getProfile();
        // this.loadDataDiaChi();

    },
    methods: {
       
        createThanhToan() {
            axios
                .post('http://127.0.0.1:8000/api/thanh-toan/key-chuyen-khoan', this.create_thanh_toan, {
                    headers : {
                        Authorization : 'Bearer ' + localStorage.getItem('chia_khoa_16')
                    }
                })
                .then((res) => {
                    if (res.data.status) {
                        toaster.success(res.data.message);
                    } else {
                        toaster.error(res.data.message);
                    }
                })
        },
        getProfile() {
            axios
                .get('http://127.0.0.1:8000/api/khach-hang/thong-tin')
                .then((res) => {
                    this.profile = res.data.data;
                   
                })
        },

        updateProfile() {
            axios
                .post('http://127.0.0.1:8000/api/khach-hang/update-thong-tin', this.profile)
                .then((res) => {
                    if (res.data.status) {
                        toaster.success(res.data.message);
                        this.getProfile()
                    } else {
                        toaster.error(res.data.message);
                    }
                })
        },

        updateMatKhau() {
            baseRequest
                .post('khach-hang/update-mat-khau', this.update_password)
                .then((res) => {
                    if (res.data.status) {
                        toaster.success(res.data.message);
                        this.getProfile()
                        this.update_password = {};
                    } else {
                        toaster.error(res.data.message);
                    }
                })
        },

        startNapTien() {
            axios
                .post('http://127.0.0.1:8000/api/khach-hang/tao-nap-tien', {}, {
                    headers : {
                        Authorization : 'Bearer ' + localStorage.getItem('chia_khoa_16')
                    }
                })  
                .then((res) => {
                    this.create_thanh_toan = res.data.data;
                })
        }


    },
}
</script>
<style></style>