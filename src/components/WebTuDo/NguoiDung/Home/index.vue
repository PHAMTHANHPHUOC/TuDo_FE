<template>
    <div class="row ">
        <div class="card" style="background-color: #ede3e3  ;">
            <div class="card-header">
                <h1><b>Danh Sách Tủ <i class="fa-solid fa-door-closed"></i></b></h1>
            </div>
            <div class="card-body">
                <div class="row">
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
                                        <div class="col-lg-8"> <button disabled class="btn btn-danger form-control ">Tủ
                                                Đã Được Thuê</button></div>
                                        <div class="col-lg-4">
                                            <button class="btn btn-info ">Trả Tủ</button>
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
                                        <h3>Thanh Toán</h3>
                                    </h1>
                                    <button type="button" class="btn-close" data-bs-dismiss="modal"
                                        aria-label="Close"></button>
                                </div>

                                <div class="modal-body">


                                    <div class="mt-2"><label for="">
                                            <h5>Thông Tin Chuyển Khoản</h5>
                                        </label>
                                        <img class="img-fluid mt-2" src="../../../../../MaQRR.jpg" alt=""><br>
                                        <h5> - Đơn vị thụ hưởng: Phạm Thanh Phước</h5>
                                        <h5> - Ngân hàng: vietcombank</h5>
                                        <h5> - Số Tài Khoản: 1023164120</h5>
                                        <h5> - Thành Tiền: {{ formatToVND(create_thanh_toan.gia_ban) }}</h5>
                                        <h5> -Nội Dung Chuyển Khoản : <b class="text-danger ">{{
                                                create_thanh_toan.pin_active }}</b></h5>
                                        <input v-model="create_thanh_toan.has_active" type="text" class="form-control"
                                            placeholder="Vui Lòng Nhập Lại Nội Dung Chuyển Khoản Tại Đây">
                                        <h3 class="text-danger ">LƯU Ý: Hãy Điền Đúng Nội Dung Chuyển Khoản Trên</h3>


                                    </div>
                                </div>

                                <div class="modal-footer">
                                    <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Hủy</button>
                                    <button v-on:click="createThanhToan()" type="button" class="btn btn-primary">Xác
                                        Nhận</button>
                                </div>
                            </div>
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
            list_tu: [],
            pin: {},
            create_thanh_toan: {},


        }
    },
    mounted() {
        this.getDataTu();
    },
    methods: {
        formatToVND(number) {
            number = parseInt(number);
            return number.toLocaleString('vi-VN', { style: 'currency', currency: 'VND' });
        },

        getDataTu() {
            axios
                .get('http://127.0.0.1:8000/api/tu-do/data')
                .then((res) => {
                    this.list_tu = res.data.data;
                })
        },

        createThanhToan() {
            axios
                .post('http://127.0.0.1:8000/api/tu-do/key-chuyen-khoan', this.create_thanh_toan)
                .then((res) => {
                    if (res.data.status) {
                        toaster.success(res.data.message);
                        this.getDataTu();


                    } else {
                        toaster.error(res.data.message);
                    }
                })
        },
        // actionThueTu(){
        //     baseRequest
        //         .post('http://127.0.0.1:8000/api/tu-do/pin', this.pin)
        //         .then((res) => {
        //             selec

        //         })
        // },

    }
}
</script>
<style></style>
