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
                                        <h5 class="card-title">{{ v.ten_san_pham }} : {{ k + 1 }}</h5>

                                    </div>
                                    <div class="col-lg-7">
                                        <h5 class="text-end" style="color: blueviolet;"> Phí:{{ formatToVND(v.gia_ban)
                                            }}</h5>
                                    </div>
                                </div>

                                <button v-if="v.is_active == 0" v-on:click="Object.assign(create_thanh_toan, v)"
                                    class="btn btn-primary form-control " data-bs-toggle="modal"
                                    data-bs-target="#thuetudo">Thuê Tủ</button>
                                <div v-else>
                                    <div class="row">
                                        <div class="col-lg-10">
                                            <button class="btn btn-danger form-control">Tủ Đã Được Thuê</button>
                                        </div>
                                        <div class="col-lg-2">
                                            <button class="form-control text-black btn btn-outline-light  "
                                                data-bs-toggle="dropdown"><i
                                                    class="fa-solid fa-caret-down"></i></button>
                                            <div class="dropdown-menu dropdown-menu-right dropdown-menu-lg-end">
                                                <a class="dropdown-item"
                                                    v-on:click="Object.assign(create_thanh_toan, v)"
                                                    data-bs-toggle="modal" data-bs-target="#pinactive">Cập Nhật Mã
                                                    Pin</a>
                                            </div>
                                        </div>
                                    </div>

                                </div>
                            </div>
                        </div>
                    </template>
                    <div class="modal fade" id="thuetudo" tabindex="-1" aria-labelledby="exampleModalLabel"
                        aria-hidden="true">
                        <div class="modal-dialog">
                            <div class="modal-content">
                                <div class="modal-header">
                                    <h1 class="modal-title fs-5" id="exampleModalLabel">
                                        <h3>Xác Nhận Thanh Toán</h3>
                                    </h1>
                                    <button type="button" class="btn-close" data-bs-dismiss="modal"
                                        aria-label="Close"></button>
                                </div>

                                <div class="modal-body">
                                    <div class="card">
                                        <div class="card-body">
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
                                                        <td><input v-model="profile.tong_tien" class="form-control"
                                                                type="text"></td>
                                                        <td><input v-model="create_thanh_toan.gia_ban"
                                                                class="form-control" type="text">
                                                        </td>
                                                    </tr>
                                                </tbody>

                                            </table>
                                        </div>
                                    </div>
                                </div>
                                <div class="modal-footer">
                                    <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Hủy</button>
                                    <button v-on:click="thanhToan(), Object.assign(update_pin_active, v)"
                                        data-bs-dismiss="modal" type="button" class="btn btn-primary">Xác
                                        Nhận</button>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
    <div class="modal fade" id="pinactive" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
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
                    <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Thoát</button>
                    <button v-on:click="updatePinActive()" type="button" class="btn btn-primary">Xác Nhận</button>
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

</style>
