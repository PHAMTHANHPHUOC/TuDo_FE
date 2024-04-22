<template>
    <div class="row ">
        <div class="card  border-primary border-3" style="background-color: #ced5dd  ;">
            <div class="card-header">
                <h1><b>Danh Sách Tủ <i class="fa-solid fa-door-closed"></i></b></h1>
            </div>
            <div class="card-body accordion-button ">
                <div class="row align-items-center">
                    <template v-for="(v, k) in list_tu">
                        <div class="col-lg-2">
                            <div class="card">
                                <img v-bind:src="v.hinh_anh" class="img-fluid" alt="...">
                            </div>
                            <div class="card-body">
                                <div class="row">
                                    <div class="col-lg-5">
                                        <h5 class="card-title">{{ v.ten_san_pham }} </h5>

                                    </div>
                                    <div class="col-lg-7">
                                        <h5 class="text-end" style="color: blueviolet;"> Phí:{{ formatToVND(v.gia_ban)
                                            }}</h5>
                                    </div>
                                </div>
                                <button v-if="v.is_active == 0" v-on:click="Object.assign(create_thanh_toan, v)"
                                    class=" btn btn-primary form-control" data-bs-toggle="modal"
                                    data-bs-target="#exampleModal">Thuê Sản Phẩm</button>
                                <button v-else class=" btn btn-danger  form-control">Tủ Đã Được Thuê</button>


                            </div>
                        </div>
                    </template>
                </div>
            </div>
        </div>
    </div>
    <!-- <div class="modal fade" id="pinactive" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                    <h1 class="modal-title fs-5" id="exampleModalLabel">Mã Pin Tủ </h1>
                    <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                </div>
                <div class="modal-body">
                    <label for="">
                        <h5> Mã Pin Hiện Tại(có thể thay đổi)</h5>
                    </label>
                    <input v-model="create_thanh_toan.pin_active" type="text" class="form-control">
                    <label for="">
                        <h5>Nhập lại Mã Pin</h5>
                    </label>
                    <input v-model="create_thanh_toan.pin_active" type="text" class="form-control">
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-secondary" >Thoát</button>
                    <button v-on:click="updatePinActive()" type="button" data-bs-dismiss="modal" class="btn btn-primary">Xác Nhận</button>
                </div>
            </div>
        </div>
    </div> -->
    <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                    <h1 class="modal-title fs-5" id="exampleModalLabel">Xác Nhận Thanh Toán</h1>
                    <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                </div>
                <div class="modal-body">
                    <table class="table table-bordered accordion ">
                        <thead>
                            <tr>
                                <th>Danh Mục</th>
                                <th>Tổng Tiền Trong Tài Khoản</th>
                                <th>Tổng Tiền Cần Thanh Toán</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr>
                                <td><b>Thuê Tủ</b></td>
                                <td>{{ formatToVND(profile.tong_tien) }}</td>
                                <td>{{ formatToVND(create_thanh_toan.gia_ban) }} </td>
                            </tr>
                        </tbody>
                    </table>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Thoát</button>
                    <button v-on:click="thanhToan()" type="button" data-bs-dismiss="modal" class="btn btn-primary">Xác
                        Nhận</button>
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
import Toasted from 'vue-toasted';
export default {
    data() {
        return {
            list_tu: [],
            pin: {},
            profile: {},
            create_thanh_toan: {},
            update_pin_active: {},
        }
    },
    mounted() {
        this.getDataTu();
        this.getProfile();
        const toaster = createToaster({
            position: "top-right",
            timeout: 20000, // Thời gian hiển thị: 5000 miligiây (5 giây)
            icon: {
                iconPack: "fontawesome",
                iconSize: "lg", // Kích thước biểu tượng lớn (lg)
            },
        });
    },
    methods: {

        formatToVND(number) {
            number = parseInt(number);
            return number.toLocaleString('vi-VN', { style: 'currency', currency: 'VND' });
        },
        getProfile() {
            baseRequest
                .get('khach-hang/thong-tin')
                .then((res) => {
                    this.profile = res.data.data;

                })
        },

        getDataTu() {
            baseRequest
                .get('tu-do/data')
                .then((res) => {
                    this.list_tu = res.data.data;
                })
        },


        thanhToan() {
            baseRequest
                .post('tu-do/thanh-toan', this.create_thanh_toan)
                .then((res) => {
                    if (res.data.status) {
                        toaster.success(res.data.message);
                        this.getDataTu();
                        this.getProfile();
                    } else {
                        toaster.error(res.data.message);
                    }
                })
        },
        updatePinActive() {
            baseRequest
                .post('khach-hang/update-ma-pin', this.create_thanh_toan)
                .then((res) => {
                    if (res.data.status) {
                        toaster.success(res.data.message);
                        this.getDataTu();
                        this.getProfile();
                    } else {
                        toaster.error(res.data.message);
                    }
                })
        },



    }
}
</script>
<style>

/* Định dạng cho card header */
.card-header {
    background-color: #949494;
    /* Màu nền */
    color: rgb(255, 255, 255);
    /* Màu chữ */
    text-align: center;
    /* Canh giữa nội dung */
}

/* Định dạng cho modal */
.modal-dialog {
    max-width: 700px;
    /* Độ rộng tối đa của modal */
}

/* Định dạng cho modal header */
.modal-header {
    background-color: #ab9bb2;
    /* Màu nền */
    color: white;
    /* Màu chữ */
    text-align: center;
    /* Canh giữa nội dung */
}

/* Định dạng cho nút Close trong modal */
.btn-close {
    color: white;
    /* Màu chữ */
}

/* Định dạng cho footer của modal */
.modal-footer {
    justify-content: space-between;
    /* Căn giữa các nút */
}

/* Định dạng cho table trong modal */
.table {
    margin-bottom: 0;
    /* Loại bỏ khoảng cách dưới cùng của table */
}

/* Định dạng cho table head */
.table th {
    background-color: #060f06;
    /* Màu nền */
    color: white;
    /* Màu chữ */
    text-align: center;
    /* Canh giữa nội dung */
}

/* Định dạng cho table body */
.table td {
    text-align: center;
    /* Canh giữa nội dung */
}

/* Định dạng cho tiêu đề của table */
.table thead th {
    vertical-align: middle;
    /* Canh giữa nội dung theo chiều dọc */
}

/* Định dạng cho nút trong table */
.table button {
    width: 100%;
    /* Độ rộng chiều ngang */
}

/* Định dạng cho ô input trong modal */
input[type="text"] {
    width: 100%;
    /* Độ rộng chiều ngang */
    padding: 8px;
    /* Khoảng cách giữa viền và nội dung trong input */
    margin-bottom: 10px;
    /* Khoảng cách giữa các input */
    border-radius: 5px;
    /* Bo tròn góc */
    border: 1px solid #ccc;
    /* Viền */
    box-sizing: border-box;
    /* Đảm bảo kích thước input không bị thay đổi */
}

/* Định dạng cho tiêu đề trong input */
input[type="text"]::placeholder {
    color: #aaa;
    /* Màu chữ */
}

/* Định dạng cho các hàng trong table */
.table tbody tr:nth-child(even) {
    background-color: #b34141;
    /* Màu nền cho các hàng chẵn */
}
</style>
