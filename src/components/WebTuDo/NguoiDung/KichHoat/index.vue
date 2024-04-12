<template >
  hehe
</template>
<script>
import baseRequest from '../../../../core/baseRequest';
import axios from 'axios';
import { createToaster } from "@meforma/vue-toaster";
const toaster = createToaster({ position: "top-right" });

export default {
    props : ['id_can_kich_hoat'],   
    data() {
        return {
            kich_hoat:'',
        }
    },
    mounted() {
        this.kich_hoat=this.$route.params.id_can_kich_hoat;
        this.KichHoat();
    },
    methods: {
        KichHoat(){
            let payload = {
                'id_can_kich_hoat' : this.kich_hoat
            }
            baseRequest
            .post('admin/khach-hang/kich-hoat-tai-khoan', payload)
            .then((res) => {
                if(res.data.status) {
                        toaster.success(res.data.message);
                        this.$router.push('/khach-hang/dang-nhap');
                    } else {
                        toaster.error(res.data.message);
                    }
            })
        }

        
    },
}
</script>
<style >
    
</style>