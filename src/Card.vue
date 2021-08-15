<template>
  <div>
    <img :src="원룸들.image" class="room-img">
    <h4 @click="send">{{원룸들.title}}</h4>
    <p>{{원룸들.price}}원</p>
  </div>
</template>

<script>
export default {
    name :'Card',
    props : {
        원룸들 : Array,
        누른거 : Number,
        모달창열렸니 : Boolean,
    },
    methods : {
        send(){
            this.$emit('openModal' , this.원룸들.id);
        }
    }
}
</script>

<style>

</style>