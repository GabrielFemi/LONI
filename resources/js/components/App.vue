<template>

 <div id="app">
     <Navbar />
     <router-view></router-view>
</div>
</template>

<script>
import Navbar from './Navbar'
export default {
    components: {
        Navbar
    },
    created() {
        this.$http.interceptors.response.use(undefined, function (err) {
            return new Promise( function (resolve, reject) {
                if (err.status === 401 && err.config && !err.config.__isRetryRequest) {
                    this.$store.dispatch('logout')
                }
            })
        })
    }


}
</script>

<style scoped>

</style>
