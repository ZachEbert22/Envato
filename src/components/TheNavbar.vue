<template>
    <nav 
        :class="[`navbar-${theme}`, `bg-${theme}`, 'navbar', 'navbar-expand-lg']">
        <div class = "container-fluid">
            <a class = "navbar-brand" href = "#">My Vue!</a>
            <ul class = "navbar-nav me-auto mb-2 mb-lg-0">
                <li v-for ="(page, index) in pages"  class= "nav-item" :key="index">
                    <the-navbar-link
                    :page="page"
                    :isActive="activePage == index"
                    @click.prevent="navLinkClick(index)"
                    >     
                    </the-navbar-link>

                </li>
            </ul>
            <form class ="d-flex">
                <button 
                class = "btn btn-primary"
                @click.prevent="changeTheme()"
                >Toggle Test</button>
            </form>
        </div>
    </nav>
</template>

<script>

import TheNavbarLink from './TheNavbarLink.vue';



export default{
    components: {
        TheNavbarLink
    },
    created(){
        this.getThemeSetting();
    },
    props:['pages', 'activePage', 'navLinkClick'],
    data(){
        return {
            theme: 'light',
        }
    },
    methods: {
        changeTheme(){
            let theme = 'light';

            if (this.theme == 'light'){
                theme = 'dark';
            }

            this.theme = theme;
            this.storeThemeSetting();
        },
        storeThemeSetting(){
            localStorage.setItem('theme', this.theme);
        },
        getThemeSetting(){
            let theme = localStorage.getItem('theme');
            if (theme){
                this.theme = theme;

            }
        },

    }
}
</script>
