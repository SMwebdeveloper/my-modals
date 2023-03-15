<template lang="">
    <div class="modal-wrapper" @click="$emit('close')">
        <div class="modal-content" @click.stop>

            <!-- header -->
            <div class="modal-header">
                <span class="modal-title">{{title}}</span>
                <span class="button-close" @click="$emit('close')">&times;</span>
            </div>

            <!-- body -->
            <div class="modal-body">
                <slot name="body">
                </slot>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    props:{
        title:{
            type: String,
            required:true
        }
    },
    mounted() {
        document.body.addEventListener('keyup', e => {
            if(e.keyCode === 27) {
                this.$emit('close')
            }
        })
    },
    computed:{},
    methods:{},
}
</script>
<style lang="css">
.modal-wrapper{
    display: flex;
    justify-content: center;
    align-items: center;
    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    transition: opacity .3s ease;
    right: 0;
    z-index: 998;
    background-color: rgba(00,00,00,.48);
}

.modal-content{
    position: relative;
    display: flex;
    flex-direction: column;
    align-content: center;
    max-width: 600px;
    padding: 20px 18px;
    background: #fff;
    border: 1px solid #dcdfe6;
    transition: all .3s ease;
    border-radius: 8px;
    z-index: 999;
    overflow: hidden;
}

.modal-content{
    display: flex;
    align-self: center;
    justify-content: space-between;
    padding-bottom: 20px;
}

.modal-content span {
    font-size: 24px;
}

.modal-content .button-close{
    cursor: pointer;
}
.modal-body{
    text-align: center;
}
.modal-header{
    display: flex;
    align-items: center;
    justify-content: space-between;
}
</style>