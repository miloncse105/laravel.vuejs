#CMD::
composer create-project --prefer-dist laravel/laravel .
npm install
npm install vue@next
npm install vue-loader@next
|
|
|
|
|
|
#FILE:: vite.config.js
import { defineConfig } from 'vite';
import vue from '@vitejs/plugin-vue'
import laravel from 'laravel-vite-plugin';
export default defineConfig({
    plugins: [
        vue(),
        laravel({
            input: ['resources/css/app.css', 'resources/js/app.js'],
            refresh: true,
        }),
    ],
});
|
|
|
|
|
|
#CREATE FILE:: resource/views/app.blade.php
<!DOCTYPE html>
<html lang="{{ str_replace('_', '-', app()->getLocale()) }}">
    <head>
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <title>Laravel</title>
        @vite(['resources/css/app.css', 'resources/js/app.js'])
    </head>

    <body>
    <div id="app"></div>
    </body>
</html>
|
|
|
|
|
|
#UPDATE:: Routes/web.php
<?php
use Illuminate\Support\Facades\Route;

Route::get('{any}', function () {
    return view('app');
})->where('any','.*');
|
|
|
|
|
|
#UPDATE:: resources/js/app.js
import './bootstrap';
import { createApp } from 'vue'
import App from './App.vue'
import router from './router.js';

const app = createApp(App);
app.use(router);
app.mount('#app');
|
|
|
|
|
|
#CREATE FILE:: resources/js/router.js
import {createWebHistory, createRouter} from "vue-router";
import home from './components/Home.vue'
import contact from './components/Contact.vue'

export const routes = [
    {
        name: 'home',
        path: '/',
        component: home
    },
    {
        name: 'contact',
        path: '/contact',
        component: contact
    }
];

const router = createRouter({
    history: createWebHistory(),
    routes: routes,
});
export default router;
|
|
|
|
|
|
#CREATE FILE:: resources/js/components/Home.vue
<template>
    <div class="home">
     <h1>{{title}}</h1>
    </div>
</template>
  
<script>
  export default {
    name: 'home',
    data () {
      return {
       title:'Home Page...'
      }
    }
  }
</script>
  
<style scoped>
  
</style>
|
|
|
|
|
|
#CREATE FILE:: resources/js/components/Contact.vue
<template>
    <div class="contact">
     <h1>{{title}}</h1>
    </div>
</template>
  
<script>
  export default {
    name: 'contact',
    data () {
      return {
       title:'Contact Page...'
      }
    }
  }
</script>
  
<style scoped>
  
</style>
|
|
|
|
|
|
#CREATE FILE:: resources/js/App.vue
<template>
<router-link to="/" class="nav-item nav-link">Home</router-link> || 
<router-link to="/contact" class="nav-item nav-link">Contact</router-link>
<router-view></router-view>
</template>
|
|
|
|
|
|
#CMD::
npm i @vitejs/plugin-vue
npm install vue-axios vue-loader vue-router vue-template-compiler

npm rum dev
php artisan serve
|
|
|
|
|
|
#CLEAN PROJECT CMD::
php artisan route:clear
php artisan cache:clear
php artisan view:clear
php artisan view:cache
php artisan config:cache
php artisan config:clear
php artisan route:cache
php artisan optimize:clear
php artisan clear-compiled
php artisan key:generate
composer dump-autoload
composer global update
|
|
|
|
|
|
#LARAVEL PHP ARTISAN CMD::
php artisan make:controller Home --resource
php artisan make:controller Home
php artisan make:model Home
php artisan make:migration create_homes
|
|
|
|
|
|
#PAGE REDIRECT TO OTHER PAGE SPECIFIC TIME::
<script>
  export default {
    created(){
      setTimeout( () => this.$router.push({ path: '/login'}), 5000);
    }
  }
</script>
