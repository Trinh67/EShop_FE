<template>
    <form @submit.prevent="submit" class="vld-parent" ref="formContainer">
        <!-- your form inputs goes here-->
        <label><input type="checkbox" v-model="fullPage">Full page?</label>
        <button type="submit">Login</button>
    </form>
</template>

<script>
    import Vue from 'vue';
    // Import component
    import Loading from 'vue-loading-overlay';
    // Import stylesheet
    import 'vue-loading-overlay/dist/vue-loading.css';
    // Init plugin
    Vue.use(Loading);

    export default {
        data() {
            return {
                fullPage: false
            }
        },
        methods: {
            // Loading
            submit() {
                let loader = this.$loading.show({
                  // Optional parameters
                  container: this.fullPage ? null : this.$refs.formContainer,
                  canCancel: true,
                  onCancel: this.onCancel,
                });
                // simulate AJAX
                setTimeout(() => {
                  loader.hide()
                },3000)                 
            },
            // Cancel Loading
            onCancel() {
              console.log('User cancelled the loader.')
            }                      
        }
    }
</script>