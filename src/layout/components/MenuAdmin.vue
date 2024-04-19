<template >
    <div class="nav-container primary-menu">
        <div class="mobile-topbar-header">
            <div>
                <img src="../../assets/images/logo-icon.png" class="logo-icon" alt="logo icon">
            </div>
            <div>
                <h4 class="logo-text">Rukada</h4>
            </div>
            <div class="toggle-icon ms-auto"><i class='bx bx-arrow-to-left'></i>
            </div>
        </div>
        <nav class="navbar navbar-expand-xl w-100">
            <ul class=" navbar-nav justify-content-start flex-grow-1 gap-1">
                <li class="nav-item">
                    
                        <a class="nav-link" >
                            <div class="parent-icon"><i class="fa-solid fa-user"></i>
                            </div>
                            <div class="menu-title">ADMIN</div>
                        </a>
                 
                </li>             
               
                <li class="nav-item">
                    <router-link to="/admin/danh-sach-tu">
                        <a class="nav-link" href="/admin/danh-sach-tu">
                            <div class="parent-icon"><i class="fa-solid fa-box"></i>
                            </div>
                            <div class="menu-title">Danh Sach Tủ</div>
                        </a>
                    </router-link>
                </li>
                <li class="nav-item">
                    <router-link to="/admin/danh-sach-khach-hang">
                        <a class="nav-link" href="/admin/danh-sach-khach-hang">
                            <div class="parent-icon"><i class="fa-solid fa-user"></i>
                            </div>
                            <div class="menu-title">Danh Sach Khách Hàng</div>
                        </a>
                    </router-link>
                </li>
                
              
            </ul>
        </nav>
    </div>
</template>
<script>
export default {

}
</script>
<style scoped>
.nav-container {
    background-color: #ced5dd; /* Màu nền của menu */
    color: #fff; /* Màu chữ của menu */
    padding: 10px 20px; /* Khoảng cách padding của menu */
}

.logo-icon {
    width: 50px; /* Kích thước của logo */
    height: auto;
}

.toggle-icon {
    cursor: pointer; /* Con trỏ khi hover vào biểu tượng toggle */
    color: #fff; /* Màu chữ của biểu tượng toggle */
}

.navbar-nav {
    list-style: none; /* Loại bỏ dấu chấm của danh sách menu */
    display: flex;
    align-items: center;
    padding: 0;
}

.nav-item {
    margin-right: 20px; /* Khoảng cách giữa các mục menu */
}

.nav-link {
    color: #fff; /* Màu chữ của các mục menu */
    text-decoration: none; /* Loại bỏ đường gạch chân của các mục menu */
}

.parent-icon {
    margin-right: 10px; /* Khoảng cách giữa biểu tượng và tiêu đề của mục menu */
}

.menu-title {
    font-weight: bold; /* Đậm chữ của tiêu đề của mục menu */
}
</style>