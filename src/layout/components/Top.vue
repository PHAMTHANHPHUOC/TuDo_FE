<template>
    <header>
        <div class="topbar d-flex align-items-center">
            <nav class="navbar navbar-expand">
                <router-link to="/">
                    <div class="topbar-logo-header">
                        <div class="">
                            <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcThw5Qyx4IY-4bLhc3UuDVsGxUzl5yWfSuwFg&s" class="logo-icon" alt="logo icon">
                        </div>
                        <div class="">
                            <router-link to="/">
                                <h4 class="logo-text">Website Tủ Đồ</h4>
                            </router-link>
                        </div>
                    </div>
                </router-link>
                <div class="mobile-toggle-menu"><i class='bx bx-menu'></i></div>
                <div class="search-bar flex-grow-1">
                    <div class="row">
                        <div class="col-lg-10">
                            <input type="text"
                                class="form-control search-control ms-3" style="width: 100%;"
                                placeholder="Type to search...">
                        </div>
                        <div class="col-lg-2">
                            <button  class="btn btn-secondary"><i
                                    class="fa-solid fa-magnifying-glass"></i></button>
                        </div>
                    </div>
                </div>
                <div class="top-menu ms-auto">
                    <ul class="navbar-nav align-items-center">
                        <li class="nav-item mobile-search-icon">
                            <a class="nav-link" href="#"> <i class='bx bx-search'></i>
                            </a>
                        </li>
                        <li class="nav-item dropdown dropdown-large">
                            <router-link to="/don-hang">
                                <a class="nav-link dropdown-toggle dropdown-toggle-nocaret position-relative">
                                    <span class="alert-count">3</span>
                                    <i class="fa-solid fa-credit-card"></i>
                                </a>
                            </router-link>
                        </li>
                        <li class="nav-item dropdown dropdown-large">
                                    <a class="nav-link dropdown-toggle dropdown-toggle-nocaret position-relative">
                                    <span class="alert-count">3</span>
                                    <i class="fa-solid fa-cart-shopping"></i>
                                </a>
                       
                        </li>
                        <li class="nav-item dropdown dropdown-large">
                            <a class="nav-link dropdown-toggle dropdown-toggle-nocaret position-relative" href="#"
                                role="button" data-bs-toggle="dropdown" aria-expanded="false"> <span
                                    class="alert-count">8</span>
                                <i class='bx bx-bell'></i>
                            </a>
                            <div class="dropdown-menu dropdown-menu-end">
                                <a href="javascript:;">
                                    <div class="msg-header">
                                        <p class="msg-header-title">Thông Báo</p>
                                    </div>
                                </a>
                                <div class="header-message-list">
                                    <a class="dropdown-item" href="javascript:;">
                                        <div class="d-flex align-items-center">
                                            <div class="user-online">
                                                <img src="../../assets/images/avatars/avatar-1.png" class="msg-avatar"
                                                    alt="user avatar">
                                            </div>
                                            <div class="flex-grow-1">
                                                <h6 class="msg-name">Daisy Anderson <span class="msg-time float-end">5
                                                        sec
                                                        ago</span></h6>
                                                <p class="msg-info">The standard chunk of lorem</p>
                                            </div>
                                        </div>
                                    </a>
                                </div>
                            </div>
                        </li>
                    </ul>
                </div>
                <div class="user-box dropdown">
                    <a class="d-flex align-items-center nav-link dropdown-toggle dropdown-toggle-nocaret" href="#"
                        role="button" data-bs-toggle="dropdown" aria-expanded="false">
                        <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTnO0uhwiK1yDASJ6SkO3SLFNU3dtIb4NMiBA&s" class="user-img" alt="user avatar">
                        <div class="user-info ps-3">
                            <p class="user-name mb-0"></p>
                            <p class="designattion mb-0"></p>
                        </div>
                    </a>
                    <ul class="dropdown-menu dropdown-menu-end">
                       
                        <li>
                            <div class="dropdown-divider mb-0"></div>
                        </li>
                        <li><a v-on:click="dangXuat()" class="dropdown-item" href="javascript:;"><i
                                    class='bx bx-log-out-circle'></i><span>Logout</span></a>
                        </li>
                        <li><a  v-on:click="dangXuatALL()" class="dropdown-item" href="javascript:;"><i
                                    class='bx bx-log-out-circle'></i><span>LogoutAll</span></a>
                        </li>
                    </ul>
                </div>
            </nav>
        </div>
    </header>
</template>
<script>
import { createToaster } from "@meforma/vue-toaster";
import baseRequest from '../../core/baseRequest';
import { Axios } from "axios";
const toaster = createToaster({ position: "top-right" });
export default {
    data() {
        return {
            
        }
    },
    methods: {

        dangXuat(){
            Axios
                .get('http://127.0.0.1:8000/api/khach-hang/dang-xuat')
                .then((res) => {
                    if(res.data.status) {
                        toaster.success(res.data.message);
                        this.$router.push('/khach-hang/dang-nhap')
                    } else {
                        toaster.error(res.data.message);
                    }
                    
                })

        },
        dangXuatALL(){
            Axios
                .get('http://127.0.0.1:8000/api/khach-hang/dang-xuat-all')
                .then((res) => {
                    if(res.data.status) {
                        toaster.success(res.data.message);
                        this.$router.push('/khach-hang/dang-nhap')
                    } else {
                        toaster.error(res.data.message);
                    }
                    
                })

        },
    },
}
</script>
<style scoped>
.topbar {
    background-color: #ced5dd; /* Màu nền của topbar */
    color: #fff; /* Màu chữ của topbar */
    padding: 10px 20px; /* Khoảng cách padding của topbar */
}

.topbar-logo-header {
    display: flex; /* Hiển thị theo kiểu flexbox */
    align-items: center; /* Căn chỉnh các phần tử theo chiều dọc */
}

.logo-icon {
    width: 50px; /* Kích thước của logo */
    height: auto;
}

.logo-text {
    margin-left: 10px; /* Khoảng cách giữa logo icon và text của logo */
    font-size: 20px; /* Kích thước của text của logo */
}
.logo-text {
    color: #000; /* Đổi màu chữ của tiêu đề sang màu đen */
}
.mobile-toggle-menu {
    cursor: pointer; /* Con trỏ khi hover vào biểu tượng toggle */
    color: #fff; /* Màu chữ của biểu tượng toggle */
}

.search-bar {
    display: flex; /* Hiển thị theo kiểu flexbox */
    align-items: center; /* Căn chỉnh các phần tử theo chiều dọc */
}

.search-control {
    border-radius: 5px; /* Độ cong góc của ô tìm kiếm */
}

.alert-count {
    position: absolute; /* Vị trí tuyệt đối */
    top: -8px; /* Khoảng cách từ trên xuống */
    right: -8px; /* Khoảng cách từ phải qua */
    background-color: red; /* Màu nền */
    color: #fff; /* Màu chữ */
    width: 20px; /* Chiều rộng */
    height: 20px; /* Chiều cao */
    border-radius: 50%; /* Độ cong góc */
    font-size: 12px; /* Kích thước chữ */
    display: flex; /* Hiển thị theo kiểu flexbox */
    justify-content: center; /* Căn chỉnh các phần tử theo chiều ngang */
    align-items: center; /* Căn chỉnh các phần tử theo chiều dọc */
}
</style>

