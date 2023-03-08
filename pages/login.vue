<template>
    <div>
        <b-navbar type="dark" variant="info">
            <b-navbar-brand href="#">SAS Task - Matheus Rocha</b-navbar-brand>
        </b-navbar>

        <b-container fluid class="w-100 w-md-50 p-5">
            <b-alert v-cloak :show="loginError" variant="danger">{{ loginErrorMessage }}</b-alert>
            <b-card class="w-100">
                <b-form @submit.prevent="tryLogin">
                    <b-form-group id="input-group-1" label="Email" label-for="input-1">
                        <b-form-input id="input-1" v-model="login.email" type="email" placeholder="Enter email" required />
                    </b-form-group>
        
                    <b-form-group id="input-group-2" label="Password" label-for="input-2">
                        <b-form-input id="input-2" v-model="login.password" type="password" placeholder="Enter password" required />
                    </b-form-group>
        
                    <b-button type="submit" variant="primary">
                        Login
                    </b-button>
                </b-form>
            </b-card>
        </b-container>
    </div>
</template>
  
<script>
export default {
    auth: 'guest',
    data() {
        return {
            login: {
                email: '',
                password: ''
            },
            loginError: false,
            loginErrorMessage: null
        }
    },
    methods: {
        async tryLogin() {
            this.clearLoginErrors()

            try {
                await this.$auth.loginWith('local', {
                    data: {
                        login: this.login
                    }
                })
                this.$router.push('/')
            } catch (error) {
                this.loginError = true
                this.loginErrorMessage = 'Invalid username or password. Please, try again.'
            }
        },
        clearLoginErrors() {
            this.loginError = false
            this.loginErrorMessage = null
        }
    }
}
</script>