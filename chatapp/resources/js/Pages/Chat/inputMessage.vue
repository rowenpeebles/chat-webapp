<template>
    <div class="relative h-10 m-1">
        <div style="border-top: 1px solid #e6e6e6;" class="grid grid-cols-6">

            <input type="text" v-model="message" @keyup.enter="sendMessage()" 
            placeholder="Say something..." class="col-span-5 border-transparent 
            focus:border-transparent focus:ring-0 p-1"/>

            <button @click="sendMessage()" class="place-self-end inline-flex items-center px-4 
            py-2 bg-gray-800 border border-transparent rounded-md 
            font-semibold text-xs text-white uppercase tracking-widest hover:bg-gray-700 active:bg-gray-900 
            focus:outline-none focus:border-gray-900 
            focus:ring focus:ring-gray-300 disabled:opacity-25 transition m-1 p-1">
                SEND 
            </button>

        </div>
    </div>
</template>

<script>
import Input from '../../Jetstream/Input.vue'
export default {
    components: { Input },
        props: ['room'],
        data: function () {
            return {
                message: ''
            }
        },
        methods: {
            sendMessage() {
                if( this.message == ' ') {
                    return;
                }
                axios.post('/chat/room/' + this.room.id + '/message', {
                    message: this.message
                })
                .then( response => {
                    if( response.status == 201 ) {
                        this.message = '';
                        this.$emit('messagesent');
                    }
                })
                .catch( error => {
                    console.log( error );
                })
            }
        }
}
</script>