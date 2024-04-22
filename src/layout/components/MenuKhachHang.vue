<template >
    <div class="nav-container primary-menu">
        <div class="mobile-topbar-header">
            <div>
                <img src="../../assets/images/logo-icon.png" class="logo-icon" alt="logo icon">
            </div>
            
            <div class="toggle-icon ms-auto"><i class='bx bx-arrow-to-left'></i>
            </div>
        </div>
        <nav class="navbar navbar-expand-xl w-100"  >
            <ul class=" navbar-nav justify-content-start flex-grow-1 gap-1">
                             
               
                <li class="nav-item">
                    <router-link to="/">
                        <a class="nav-link" href="/">
                            <div class="parent-icon"><i class="fa-solid fa-house"></i>
                            </div>
                            <div class="menu-title">Trang Chủ</div>
                        </a>
                    </router-link>
                </li>
                <li class="nav-item">
                    <router-link to="/khach-hang/nap-tien">
                        <a class="nav-link" href="/khach-hang/nap-tien">
                            <div class="parent-icon"><i class="fa-solid fa-qrcode"></i>
                            </div>
                            <div class="menu-title">Thông Tin Thanh Toán</div>
                        </a>
                    </router-link>
                </li>
                <li class="nav-item">
                    <router-link to="/khach-hang/hoa-don">
                        <a class="nav-link" href="/khach-hang/hoa-don">
                            <div class="parent-icon"><i class="fa-solid fa-money-bill"></i>
                            </div>
                            <div class="menu-title">Hóa Đơn Thanh Toán</div>
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
<style>
/* Định dạng chung cho menu */
.nav-container.primary-menu {
  background-color: #b9c1ca; /* Màu nền */
  padding: 10px; /* Khoảng cách lề */
}

/* Định dạng cho logo */
.logo-icon {
  width: 40px; /* Kích thước */
  height: auto; /* Đảm bảo tỉ lệ khung hình được giữ */
}

/* Định dạng cho icon toggle */
.toggle-icon {
  cursor: pointer; /* Con trỏ khi di chuột qua */
}

/* Định dạng cho menu */
.navbar {
  padding: 0; /* Xóa khoảng cách lề */
}

/* Định dạng cho danh sách menu */
.navbar-nav {
  display: flex; /* Hiển thị theo chiều ngang */
  align-items: center; /* Canh giữa các phần tử */
}

/* Định dạng cho mỗi mục menu */
.nav-item {
  list-style: none; /* Ẩn dấu chấm liệt kê */
}

/* Định dạng cho link */
.nav-link {
  text-decoration: none; /* Ẩn gạch chân */
  color: #333; /* Màu chữ */
  display: flex; /* Hiển thị theo chiều ngang */
  align-items: center; /* Canh giữa các phần tử */
}

/* Định dạng cho icon và tiêu đề mục menu */
.parent-icon {
  margin-right: 5px; /* Khoảng cách với tiêu đề */
}

/* Định dạng cho tiêu đề mục menu */
.menu-title {
  font-weight: bold; /* Đậm */
}

</style>
