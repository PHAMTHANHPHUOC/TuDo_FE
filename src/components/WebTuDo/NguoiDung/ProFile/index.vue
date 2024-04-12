<template>
    <div class="row">
        <div class="col-lg-6">
            <div class="card">
                <div class="card-body">
                    <div class="d-flex flex-column align-items-center text-center">
                        <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTnO0uhwiK1yDASJ6SkO3SLFNU3dtIb4NMiBA&s"
                            alt="Quản trị viên" class="rounded-circle p-1 bg-primary" width="110">
                        <div class="mt-3">
                            Tên:Phước
                        </div>
                    </div>
                    <hr class="my-4">
                    <button  class="btn btn-outline-info " v-on:click="startNapTien()"
                        data-bs-toggle="modal" data-bs-target="#NapTientk">Nạp Tiền</button>
                </div>
            </div>
        </div>
        <!-- <div  class="col-lg-8">
            <div class="card">
                <div class="card-body">
                    <div class="row mb-3">
                        <div class="col-sm-3">
                            <h6 class="mb-0">Full Name</h6>
                        </div>
                        <div class="col-sm-9 text-secondary">
                            <input v type="text" class="form-control" >
                        </div>
                    </div>
                    <div class="row mb-3">
                        <div class="col-sm-3">
                            <h6 class="mb-0">Email</h6>
                        </div>
                        <div class="col-sm-9 text-secondary">
                            <input type="text" class="form-control" value="john@example.com">
                        </div>
                    </div>
                    <div class="row mb-3">
                        <div class="col-sm-3">
                            <h6 class="mb-0">Phone</h6>
                        </div>
                        <div class="col-sm-9 text-secondary">
                            <input type="text" class="form-control" value="(239) 816-9029">
                        </div>
                    </div>
                    <div class="row mb-3">
                        <div class="col-sm-3">
                            <h6 class="mb-0">Mobile</h6>
                        </div>
                        <div class="col-sm-9 text-secondary">
                            <input type="text" class="form-control" value="(320) 380-4539">
                        </div>
                    </div>
                    <div class="row mb-3">
                        <div class="col-sm-3">
                            <h6 class="mb-0">Address</h6>
                        </div>
                        <div class="col-sm-9 text-secondary">
                            <input type="text" class="form-control" value="Bay Area, San Francisco, CA">
                        </div>
                    </div>
                    <div class="row">
                        <div class="col-sm-3"></div>
                        <div class="col-sm-9 text-secondary">
                            <button v-on:click="updateProfile()" class="btn btn-primary "> Xác Nhận</button>
                        </div>
                    </div>
                </div>
            </div>
        </div> -->
    </div>
    <div class="modal fade" id="NapTientk" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                    <h1 class="modal-title fs-5" id="exampleModalLabel">Nạp Tiền</h1>
                    <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                </div>
                <div class="modal-body">
                    <div class="mt-2"><label for="">
                            <h5>Thông Tin Chuyển Khoản</h5>
                        </label>
                        <img class="img-fluid mt-2" src="../../../../../MaQRR.jpg" alt=""><br>
                        <h5> - Đơn vị thụ hưởng: Phạm Thanh Phước</h5>
                        <h5> - Ngân hàng: vietcombank</h5>
                        <h5> - Số Tài Khoản: 1023164120</h5>
                        <h5> -Nội Dung Chuyển Khoản : <b class="text-danger ">{{ create_thanh_toan.pin_active }}</b></h5>
                        <input v-model="create_thanh_toan.hash_active" type="text" class="form-control"
                            placeholder="Vui Lòng Nhập Lại Nội Dung Chuyển Khoản Tại Đây">
                            <label for="">Vui Lòng Nhập Số Tiền Cần Nạp</label>
                        <input v-model="create_thanh_toan.thanh_tien" type="text" class="form-control"
                            placeholder="Vui Lòng Nhập Lại Nội Dung Chuyển Khoản Tại Đây">
                        <h3 class="text-danger ">LƯU Ý: Hãy Điền Đúng Nội Dung Chuyển Khoản Trên</h3>
                    </div>
                    <div class="modal-footer">
                        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">thoát</button>
                        <button v-on:click="createThanhToan()" type="button" class="btn btn-primary">Xác Nhận</button>
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
            create_thanh_toan:{}

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
            baseRequest
                .get('khach-hang/thong-tin')
                .then((res) => {
                    this.profile = res.data.data;
                })
        },

        updateProfile() {
            baseRequest
                .post('khach-hang/update-thong-tin', this.profile)
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