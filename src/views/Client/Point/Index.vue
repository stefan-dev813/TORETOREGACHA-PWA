<template>
    <AdminLayout>
        <div class="pt-6 md:px-2 px-4" style="min-height:400px;">  
            <h1 class="mb-10 font-bold text-center text-lg underline underline-offset-8 mb-4">&nbsp;&nbsp;&nbsp;ポイントを購入する&nbsp;&nbsp;&nbsp;</h1>
            <div class="grid md:grid-cols-4 sm:grid-cols-3 grid-cols-2 md:px-9 px-3 justify-center gap-4 pb-8">
                <template v-for="(point, key) in points">
                    <a :href="purchase_url + '/' + point.id" class="flex flex-col justify-between cursor-pointer border-2 border-solid border-gray-2000 bg-white text-center relative rounded-lg overflow-hidden">
                        <div class="text-center flex justify-center w-full">
                            <img class="inline-block object-cover w-full -my-[10%]" :src="point.image"/> 
                        </div>
                        <div class="flex-1 flex flex-wrap w-full px-2 justify-between gap-2 items-center min-h-[3rem] relative bg-[#896858]" style="z-index: 1;">
                            <span class="text-xs flex items-center justify-center text-white font-bold text-center flex-1">
                                {{point.title}}
                            </span>
                            <div class="flex-1 flex justify-center">
                                <button class="rounded-full py-0.3 h-fit bg-white px-3 font-bold text-xs">
                                    ¥&nbsp;{{point.amount_str}}
                                </button>

                            </div>
                        </div>
                    </a>
                </template>
            </div>
        </div>

    </AdminLayout>
</template>

<script>
import AdminLayout from '../../Layout/Admin.vue';
import axios from 'axios';
import { mapActions } from 'vuex';
import { SERVER_URL } from '../../../config';

export default {
    components: {AdminLayout},
    setup() {
        document.title = 'ポイントを購入する - とれとれガチャステーション';
    },
    data() {
        return {
            is_busy: false,
            is_admin: false,
            purchase_url: 'purchase',
            points: []
        }
    },
    async created() {
        try {
            const response = await axios.get(`/api/points`);
            this.points = response.data.points; // Adjust this line based on your actual API response structure
        } catch (error) {
            console.error('Error fetching points:', error);
        }
    },
    methods : {
        // checkout(id) {
        //     this.is_busy = true;
        //     const post_data = { id: id };
        //     axios.post(route('user.point.checkouturl'), post_data)
        //     .then(response=>{ 
        //         this.is_busy = false;
        //         if(response.status == 201 || response.status == 200) {
                    
        //             if(response.data.status) {
        //                 console.log(response.data.status);
        //                 window.location.href = response.data.url;
        //             } else {
        //                 alert('サーバーが混み合っております。少し時間をおいて再度お試しください。');        
        //             }
        //         } else {
        //             alert('サーバーが混み合っております。少し時間をおいて再度お試しください。');
        //         }
        //     }).catch(error=> {
        //         this.is_busy = false;
        //         // alert('サーバーが混み合っております。少し時間をおいて再度お試しください。');
        //     });
        // }
    },
    mounted() {
        // if (this.auth.user) {
        //     if (this.auth.user.type==1) {
        //         this.is_admin = true;
        //         this.purchase_uri = 'test.user.point.purchase';
        //     }
        // },
    }
}
</script>