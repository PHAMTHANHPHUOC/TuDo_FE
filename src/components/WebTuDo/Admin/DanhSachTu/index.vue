<template>
    <div class="card">
        <div class="card-header">
            <div class="row">
                <div class="col-lg-11">
                    <h3>Danh Mục Sản Phẩm</h3>
                </div>
                <div class="col-lg-1">
                    <button v-on:click="Object.assign(create_tu)" class="btn btn-outline-info  text-end" data-bs-toggle="modal"
                        data-bs-target="#ThemTuDo">Thêm Tủ Mới</button>

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
                            <th class="text-center">Password Chuyển Khoản</th>
                            <th class="text-center"> Trạng Thái </th>
                            <th class="text-center">Tình Trạng</th>
                            <th class="text-center">AcTion</th>

                        </tr>
                    </thead>
                    <template v-for="(v, k) in list_tu">
                        <tbody>
                            <tr>
                                <td class=" text-center"> Tủ Số :{{ k + 1 }}</td>
                                <td class=" text-center"><img class="img-fluid " style="height: 50px; width: 50px;"
                                        v-bind:src="v.hinh_anh" alt=""></td>
                                <td class=" text-center">{{ v.gia_ban }}</td>
                                <td class=" text-center">{{ v.pin_active }}</td>
                                <td class=" text-center">
                                  
                                    <button v-if="v.has_active == v.pin_active" class="btn btn-primary">Đã Xác Nhận</button>
                                    <button v-else class="btn btn-danger"> Chưa Xác Nhận</button>
                                </td>
                                <td class="mt-2 text-center">
                                    <button v-if="v.is_active == 0" class="btn btn-primary" style="width: 250px;">Tủ
                                        Trống</button>
                                    <button v-else class="btn btn-danger" style="width: 250px;">Đã Được Sử
                                        Dụng</button>
                                </td>
                                <td class="text-center">
                                    <button class="btn btn-primary m-2">Cập Nhật</button>
                                    <button class="btn btn-danger ">Xóa</button>
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
                    <input v-model="create_tu.ten_san_pham"  type="text" class="form-control " placeholder="">
                    <label for="">Hình Anh</label>
                    <input v-model="create_tu.hinh_anh"  type="text" class="form-control " placeholder="">
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
                    <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
                    <button v-on:click="createTuDo()" type="button" class="btn btn-primary">Thêm</button>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import axios from 'axios'
import { createToaster } from "@meforma/vue-toaster";
const toaster = createToaster({ position: "top-right" });
axios
export default {
    data() {
        return {
            list_tu: [],
            create_tu: {}
            // delete_danh_muc: {},
        }
    },
    mounted() {
        this.LoadTuDo()
    },
    methods: {
        LoadTuDo() {
            axios
                .get('http://127.0.0.1:8000/api/tu-do/data')
                .then((res) => {
                    this.list_tu = res.data.data
                })

        },
        createTuDo() {
            axios
                .post('http://127.0.0.1:8000/api/tu-do/create', this.create_tu)
                .then((res) => {
                    if (res.data.status) {
                        toaster.success(res.data.message);
                        this.LoadTuDo();
                    } else {
                        toaster.error(res.data.message);
                    }
                })

        },


    },

}
</script>
<style></style>