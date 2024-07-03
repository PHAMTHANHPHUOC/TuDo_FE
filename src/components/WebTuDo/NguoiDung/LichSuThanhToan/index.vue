<!-- <template>
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
                        <th>Mã Hóa Đơn</th>
                     </tr>
                  </thead>
                  <tbody>
                     <template v-for="(v, k) in list_hoa_don">
                        <tr>
                           <td>{{ k + 1 }}</td>
                           <td>{{ v.tong_tien_thanh_toan }}</td>
                           <td>{{ v.ma_don_hang }}</td>
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
            .get('khach-hang/lich-su-thanh-toan')
            .then((res) => {
               this.list_hoa_don = res.data.data;
            })
      },
   },
}
</script>
<style></style> -->