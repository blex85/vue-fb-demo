<template>
    <div class='admin'>
        <my-header></my-header>

        <div class='admin-main'>
            <div class='admin-main-right'>
                <el-menu theme="dark" class="top-menu">
                    <el-submenu index="1">
                        <template slot="title">商品管理</template>
                        <router-link to="/admin/goods-list">
                            <el-menu-item index="1-1">商品列表</el-menu-item>
                        </router-link>

                        <router-link to="/admin/goods-form">
                            <el-menu-item index="1-2">新增商品</el-menu-item>
                        </router-link>
                    </el-submenu>

                    <el-submenu index="2">
                        <template slot="title">用户管理</template>
                        <el-menu-item index="2-1"
                                      @click="controlJump('/admin/user-list')">用户列表
                        </el-menu-item>

                        <el-menu-item index="2-2"
                                      @click="controlJump('/admin/user-form')">新增用户
                        </el-menu-item>
                    </el-submenu>
                </el-menu>
            </div>

            <div class='admin-main-left'>
                <router-view></router-view>
            </div>

        </div>
    </div>
</template>

<script>
    import Header from './common/header.vue';

    export default {
        name: 'admin',

        components: {
            'my-header': Header,
        },

        computed: {
            user () {
                return this.$store.state.user;
            },
        },

        methods: {
            // 跳转控制
            controlJump (target) {
                if (this.user.role < 10) {
                    this.$message.warning('权限不够，努力升级');

                } else {
                    this.$router.push(target);
                }

            }
        },

    }
</script>