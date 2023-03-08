<template>
    <div>
        <b-navbar toggleable="lg" type="dark" variant="info">
            <b-navbar-brand href="#">SAS Task - Matheus Rocha</b-navbar-brand>

            <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

            <b-collapse id="nav-collapse" is-nav>
                <b-navbar-nav class="ml-auto">
                    <b-nav-item-dropdown right>
                        <template #button-content>
                            <em>SAS Task</em>
                        </template>
                        <b-dropdown-item @click="openLinkedin">My LinkedIn</b-dropdown-item>
                        <b-dropdown-item @click="logout">Logut</b-dropdown-item>
                    </b-nav-item-dropdown>
                </b-navbar-nav>
            </b-collapse>
        </b-navbar>
    </div>
</template>

<script>
export default {
    methods: {
        async logout() {
            await this.$auth.logout()
            this.$router.push('/login')
        },
        openLinkedin() {
            open("https://www.linkedin.com/in/rocha-matheus/?locale=en_US", "_blank")
        }
    }
}
</script>