<template>
    <el-Dialog v-model="dialogVisible" title="添加剧院" width="50%" :before-close="handleClose">
        <el-form label-width="70px" :model="addForm" ref="addForm">
            <el-form-item label="剧院名称">
                <el-input v-model="addForm.TheaterName"></el-input>
            </el-form-item>
            <el-form-item label="剧院地址">
                <el-input v-model="addForm.Address"></el-input>
            </el-form-item>
            <el-form-item label="剧院容量">
                <el-input v-model="addForm.Capacity"></el-input>
            </el-form-item>
        </el-form>
        <el-button @click="dialogVisible = false">取消</el-button>
        <el-button type="primary" @click="sureSubmit">
            确定
        </el-button>
    </el-Dialog>
</template>

<script>
import { ref } from 'vue'
import { ElMessageBox } from 'element-plus'
import eventBus from "@/utils/eventBus.js";
import { mapState, mapGetters } from 'vuex';
const dialogVisible = ref(false)

export default {
    computed: {
        ...mapGetters('adminlogin', ['getAdminID']),
        ...mapState('adminogin', ['user']),
    },
    mounted() {
        const addFormHandle = this.addFormHandle;
        eventBus.on("onAddEvent", addFormHandle);
        this.addForm.AdminID = this.getAdminID
        // console.log("UserID from Vuex:", this.getAdminID);
    },
    methods: {
        handleClose(done) {
            ElMessageBox.confirm('确定关闭对话框？')
                .then(() => {
                    done()
                })
                .catch(() => {
                    // catch error
                })
        },
        addFormHandle(flag) {
            this.dialogVisible = flag;
        },
        sureSubmit() {
            console.log(this.addForm)
            this.$api.addTheater(this.addForm).then((res) => {
                console.log(res.data);
                if (res.data.code == 2000) {
                    // this.clearForm();
                    this.dialogVisible = false;
                    eventBus.emit("onAddSuccess");
                    this.$message({
                        message: "添加成功",
                        type: "success"
                    });
                } else {
                    this.$message({
                        message: "添加失败",
                        type: "error"
                    });
                }
            });
        }
    },
    data() {
        return {
            dialogVisible: false,
            addForm: {
                TheaterName: "",
                Address: "",
                Capacity: "",
                AdminID: "",
            }
        }
    }
}

</script>

<style scoped>
/* Your styles here */
</style>
