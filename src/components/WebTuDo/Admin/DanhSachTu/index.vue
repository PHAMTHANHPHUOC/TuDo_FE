<template>
    <div class="card">
        <div class="card-header">
            <div class="row">
                <div class="col-lg-11">
                    <h3>Danh Mục Sản Phẩm</h3>
                </div>
                <div class="col-lg-1">
                    <button v-on:click="Object.assign(create_tu , v)" class="btn btn-outline-info  text-end"
                        data-bs-toggle="modal" data-bs-target="#ThemTuDo">Thêm Tủ Mới</button>

                </div>
            </div>
        </div>
        <div class="card-body">
            <div class="table">
                <table class="table table-bordered  ">
                    <thead>
                        <tr>
                            <th class="text-center">STT Tủ</th>
                            <th class="text-center">Hình Anh</th>
                            <th class="text-center">Giá Bán</th>
                            <th class="text-center">Password Tủ Đồ</th>
                            <th class="text-center">Tình Trạng</th>
                            <th class="text-center">AcTion</th>

                        </tr>
                    </thead>
                    <template v-for="(value, k) in list_tu">
                        <tbody>
                            <tr>
                                <td class=" text-center"> Tủ Số :{{ k + 1 }}</td>
                                <td class=" text-center"><img class="img-fluid " style="height: 50px; width: 50px;"
                                        v-bind:src="value.hinh_anh" alt=""></td>
                                <td class=" text-center">{{ formatToVND(value.gia_ban) }}</td>
                                <td class=" text-center">{{ value.pin_active }}</td>

                                <td class="mt-2 text-center">
                                    <button v-on:click="changeTrangThai(value)" v-if="value.is_active == 0" class="btn btn-primary" style="width: 250px;">Tủ
                                        Trống</button>
                                    <button v-on:click="changeTrangThai(value)" v-else class="btn btn-danger" style="width: 250px;">Đã Được Sử
                                        Dụng</button>
                                </td>
                                <td class="text-center">
                                    <button v-on:click="Object.assign(update_tu , value)" class="btn btn-primary m-2"
                                        data-bs-toggle="modal" data-bs-target="#uptadetu">Cập Nhật</button>
                                    <button v-on:click="Object.assign(delete_tu,value)" class="btn btn-danger "
                                        data-bs-toggle="modal" data-bs-target="#exampleWarningModal">Xóa</button>
                                </td>
                            </tr>
                        </tbody>
                    </template>
                </table>
            </div>

        </div>
    </div>
    <div class="modal fade" id="ThemTuDo" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                    <h1 class="modal-title fs-5" id="exampleModalLabel">Thêm Tủ Đồ</h1>
                    <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                </div>
                <div class="modal-body">
                    <label for="">Tên Tủ</label>
                    <input v-model="create_tu.ten_san_pham" type="text" class="form-control " placeholder="">
                    <label for="">Hình Anh</label>
                    <input v-model="create_tu.hinh_anh" type="text" class="form-control " placeholder="">
                    <label for="">Giá Bán</label>
                    <input v-model="create_tu.gia_ban" type="text" class="form-control " placeholder="">
                    <label for="">Password Chuyển Khoản</label>
                    <input v-model="create_tu.pin_active" type="text" class="form-control " placeholder="">
                    <label for="">Trạng Thái</label>
                    <input v-model="create_tu.has_active" type="text" class="form-control " placeholder="">
                    <label>Tình Trạng</label>
                    <select v-model="create_tu.is_active" class="form-control mt-1">
                        <option value="1">Đã Được Sử Dụng</option>
                        <option value="0">Tủ Trống</option>
                    </select>

                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Thoát</button>
                    <button v-on:click="createTuDo()" data-bs-dismiss="modal"  type="button" class="btn btn-primary">Xác Nhận</button>
                </div>
            </div>
        </div>
    </div>
    <div class="modal fade" id="uptadetu" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                    <h1 class="modal-title fs-5" id="exampleModalLabel">Cập Nhật Tủ</h1>
                    <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                </div>
                <div class="modal-body">
                    <label for="">Tên Tủ</label>
                    <input v-model="update_tu.ten_san_pham" type="text" class="form-control " placeholder="">
                    <label for="">Hình Anh</label>
                    <input v-model="update_tu.hinh_anh" type="text" class="form-control " placeholder="">
                    <label for="">Giá Bán</label>
                    <input v-model="update_tu.gia_ban" type="text" class="form-control " placeholder="">
                    <label for="">Password Chuyển Khoản</label>
                    <input v-model="update_tu.pin_active" type="text" class="form-control " placeholder="">
                    <label>Tình Trạng</label>
                    <select v-model="update_tu.is_active" class="form-control mt-1">
                        <option value="1">Đã Được Sử Dụng</option>
                        <option value="0">Tủ Trống</option>
                    </select>

                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Thoát</button>
                    <button v-on:click="updateTu()" data-bs-dismiss="modal"  type="button" class="btn btn-primary">Xác Nhận</button>
                </div>
            </div>
        </div>
    </div>
    <div class="modal fade" id="exampleWarningModal" tabindex="-1" aria-hidden="true" style="display: none;">
        <div class="modal-dialog modal-lg modal-dialog-centered">
            <div class="modal-content bg-warning">
                <div class="modal-header border-dark">
                    <h5 class="modal-title text-dark">Xóa Tủ</h5>
                    <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                </div>
                <div class="modal-body text-dark">
                    <div class="alert alert-warning border-0 bg-warning alert-dismissible fade show py-2">
                        <div class="d-flex align-items-center">
                            <div class="font-35 text-dark"><i class="bx bx-info-circle"></i>
                            </div>
                            <div class="ms-3">
                                <h6 class="mb-0 text-dark">Thông Báo</h6>
                                <div class="text-dark">
                                    Bạn có chắc chắn muốn xóa Tủ này
                                    không?

                                    <h5 class="text-danger ">Lưu ý: Thao Tác Này Không Thể Hoàn Tác</h5>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="modal-footer border-dark">
                    <button type="button" class="btn btn-light" data-bs-dismiss="modal">Thoát</button>
                    <button v-on:click="deleteTu()" data-bs-dismiss="modal"  type="button" class="btn btn-dark">Xác Nhận</button>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import axios, { Axios } from 'axios'
import { createToaster } from "@meforma/vue-toaster";
import baseRequest from '../../../../core/baseRequest';
const toaster = createToaster({ position: "top-right" });
axios
export default {
    data() {
        return {
            list_tu: [],
            create_tu: {},
            update_tu: {},
            delete_tu :{}
            // delete_danh_muc: {},
        }
    },
    mounted() {
        this.LoadTuDo()
    },
    
    methods: {
        formatToVND(number) {
            number = parseInt(number);
            return number.toLocaleString('vi-VN', { style: 'currency', currency: 'VND' });
        },  
        LoadTuDo() {
            baseRequest
                .get('tu-do/data')
                .then((res) => {
                    this.list_tu = res.data.data
                })

        },
        createTuDo() {
            baseRequest
                .post('tu-do/create', this.create_tu)
                .then((res) => {
                    if (res.data.status) {
                        toaster.success(res.data.message);
                        this.LoadTuDo();
                    } else {
                        toaster.error(res.data.message);
                    }
                })

        },
        updateTu() {
            baseRequest
                .post('tu-do/update', this.update_tu)
                .then((res) => {
                    if (res.data.status) {
                        toaster.success(res.data.message);
                        this.LoadTuDo();
                    } else {
                        toaster.error(res.data.message);
                    }
                })

        },
        deleteTu() {
            baseRequest
                .delete('tu-do/delete/'+this.delete_tu.id)
                .then((res) => {
                    if(res.data.status) {
                        toaster.success('Thông báo<br>' + res.data.message);
                        this.LoadTuDo();
                    } else {
                        toaster.error('Thông báo<br>' + res.data.message);
                    }
                })
        },
        changeTrangThai(value) {
            baseRequest
                .post('tu-do/change-status', value)
                .then((res) => {
                    if(res.data.status) {
                        toaster.success('Thông báo<br>' + res.data.message);
                        this.LoadTuDo();
                    } else {
                        toaster.error('Thông báo<br>' + res.data.message);
                    }
                });
        },


    },

}
</script>
<style></style>