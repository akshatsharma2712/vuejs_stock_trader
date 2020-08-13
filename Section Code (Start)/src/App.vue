<template>
    <div class="container">
        <app-header></app-header>
        <div class="row">
            <div class="col-md-12">
                <transition name="slide" mode="out-in">
                    <router-view></router-view>
                </transition>                
            </div>
        </div>
      

    </div>
</template>

<script>
import Header from './component/Header.vue'

    export default {
        components:{
            appHeader: Header
        },
        created()
        {
            this.$store.dispatch('initStocks');
        }
    }
</script>

<style>
body{
    padding:30px;
    background-image: url(https://images.unsplash.com/photo-1583752028088-91e3e9880b46?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1934&q=80);
    background-repeat: no-repeat;
  background-size: 1300px 800px;
}

.slide-enter-active {
    animation: slide-in 200ms ease-out forwards;

}
.slide-leave-active{
  animation: slide-out 200ms ease-out forwards;
}
@keyframes slide-in{
    from{
         transform: translateY(-30px);
         opacity: 0;
    }
    to{
        transform: translateY(0px);
        opacity: 1;
    }
}
@keyframes slide-out{
    from {
    transform: translateY(0);
    opacity: 1;
    }
    to{
          transform: translateY(-30px);
          opacity: 0;
    }
}

</style>
