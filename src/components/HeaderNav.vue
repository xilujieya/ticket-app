<template>
    <el-menu :default-active="activeIndex" class="el-menu" mode="horizontal" @select="handleSelect"
        background-color="#545c64" text-color="#fff" active-text-color="#ffd04b" router>
        <el-menu-item index="/">首页</el-menu-item>
        <el-menu-item index="/concert">演出</el-menu-item>
        <el-menu-item index="/ticket">票务</el-menu-item>
        <div class="flex-grow" />
        <el-menu-item index="login">登录</el-menu-item>
        <el-menu-item index="login">注册</el-menu-item>
        <el-sub-menu index="3">
            <template #title>个人中心</template>
            <el-menu-item index="/information">个人信息</el-menu-item>
            <el-menu-item index="/" @click="logoutHandle">注销</el-menu-item>
        </el-sub-menu>
    </el-menu>
</template>
  
<script>
import { mapMutations } from "vuex"
import { ref } from 'vue'

export default {
    data() {
        return {
            activeIndex: "1",
        };
    },
    methods: {
        ...mapMutations("users", ["setAuthentication"]),
        handleSelect(key, keyPath) {
            sessionStorage.setItem("activeIndex", key);
            console.log(key, keyPath);

        },

        logoutHandle() {
            // this.setUser({})
            localStorage.removeItem("ticket");
            this.$store.dispatch('logout');
            this.$router.push("/login")
        }
    },
    mounted() {
        if (sessionStorage.getItem("activeIndex"))
            this.activeIndex = sessionStorage.getItem("activeIndex");
    }
};
</script>
  
<style>
.flex-grow {
    flex-grow: 1;
}
</style>
  