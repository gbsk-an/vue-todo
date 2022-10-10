<template>
<div class="popup modal" v-if="show" @click.stop="hideModal">
    <div class="modal-dialog">
        <div class="modal-content" @click.stop>
            <div class="modal-header">
                <h5 class="modal-title" id="staticBackdropLabel">Modal title</h5>
                <button 
                    type="button" 
                    class="btn-close" 
                    aria-label="Close"
                    @click.stop="hideModal"
                >
                </button>
              </div>
            <div class="modal-body">
                <slot>
            
                </slot>
            </div>                
        </div>            
    </div>
</div>
</template>

<script>
export default {
    name: 'modal',
    props: {
        show: {
            type: Boolean,
            default: false
        }
    },
    methods: {
        hideModal() {
            this.$emit('update:show', false)
        }
    }
}
</script>

<style lang="scss" scoped>
.popup {
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    position: fixed;
    background-color: rgba(0, 0, 0, 0.5);
    display: flex;
}
</style>