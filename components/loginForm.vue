<template>
    <form class = 'loginRegisterForm' @submit.prevent = "handleFormSubmit()">
        <div class = 'loginRegisterForm__contentWrapper'>
            <textInput 
                :defaultValue = "emailInputValue"
                @input-update = "updateEmail"
                name = "Email"
                />

            <textInput 
                :defaultValue = "passwordInputValue"
                @input-update = "updatePassword"
                :hidden = "true"
                name = "Password"
                />
                
            <p class = 'loginRegisterForm__contentWrapper__paragraph'>
                Don't have account yet? <NuxtLink to = "/register"> Go to register </NuxtLink> 
            </p>
        </div>
        <submitBtn btnText = 'Login' />
    </form>
</template>

<script>
import textInput from './textInput';
import submitBtn from './submitBtn';

export default {
    components: {
        textInput,
        submitBtn,
    },

    data(){
        return({
            emailInputValue: '',
            passwordInputValue: '',
        })
    },

    methods:{
        updateEmail(value){
            this.emailInputValue = value;
        },

        updatePassword(value){
            this.passwordInputValue = value;
        },

        handleFormSubmit(){
            this.$store.dispatch('userStore/loginUser', {email: this.emailInputValue, password: this.passwordInputValue})
            if( this.$store.state.userStore.login.success ){
                this.$router.push('/');
            }
            else
                if(!process.server)
                    alert('User with this combination not found. Check email and password then try again');
        }
    }

    }
</script>
<style scoped lang = 'scss'>
@import '../assets/globalScss/globals.scss';
@import '../assets/globalScss/animations.scss';
@import './styles/loginRegisterFormStyles.scss';

</style>