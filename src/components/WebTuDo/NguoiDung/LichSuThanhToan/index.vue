<template>
<div class="row">
   <div class="col-lg-12">
      <div class="card">
         <div class="card-header">
            <h1>Hóa Đơn Thanh Toán</h1>
         </div>
         <div class="card-body">
            <table class="table table-bordered accordion-flush accordion-collapse  ">
               <thead>
                  <tr>
                     <th>stt</th>
                     <th>Thành Tiền</th>
                     <th>Nội Dung Chuyển Khoản</th>
                     <th>POS</th>
                     <th>Thời Gian</th>
                  </tr>
               </thead>
               <tbody>
                 <template v-for="(v,k) in list_hoa_don">
                  <tr>
                     <td>{{ k+1 }}</td>
                     <td>{{ v.creditAmout }}</td>
                     <td>{{ v.description }}</td>
                     <td>{{ v.pos }}</td>
                     <td>{{ v.created_at }}</td>
                  </tr>
                 </template>
               </tbody>

            </table>
         </div>
      </div>
   </div>
</div>


</template>
<script>
import baseRequestUser from '../../../../core/baseRequestUser';
import axios from 'axios';
import { createToaster } from "@meforma/vue-toaster";
const toaster = createToaster({ position: "top-right" });
export default {
   data() {
    return {
      list_hoa_don: []
        
    }
   },
   mounted() {
      this.getDataHoaDon()
    
   },
   methods: {
      getDataHoaDon() {
            baseRequestUser
                .get('khach-hang/hoa-don-thanh-toan')
                .then((res) => {
                    this.list_hoa_don = res.data.data;
                })
        },

    
   },

}
</script>
<style></style>