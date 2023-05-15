<template>
    <div>
        <DashboardMenu />
        <main class="main-container">
            <Loading :active="isLoading" :is-full-page="true" :can-cancel="false" />
            <div class="flex items-center mb-4 text-green-700 font-bold text-lg uppercase">
                <ThemifyIcon icon="menu" />
                <h1 class="ml-2">Account management</h1>
            </div>
            <!-- <div>
                <div class="mb-2 text-md font-medium text-gray-900 flex items-center">
                    <ThemifyIcon icon="settings" />
                    <p class="ml-2">Update Score Student manually:</p>
                </div>
                <div class="grid gap-6 mb-6 md:grid-cols-2">
                    <div>
                        <label class="block mb-2 text-sm font-medium text-gray-900 dark:text-gray-300">Full name</label>
                        <input
                            v-model="id_student"
                            type="text"
                            class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5"
                            placeholder="Fullname"
                            required=""
                        />
                    </div>
                    <div>
                        <label class="block mb-2 text-sm font-medium text-gray-900 dark:text-gray-300">Full name</label>
                        <input
                            v-model="id_course"
                            type="text"
                            class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5"
                            placeholder="Fullname"
                            required=""
                        />
                    </div>
                </div>
                <div class="grid gap-6 mb-6 md:grid-cols-2">
                    <div>
                         <label class="block mb-2 text-sm font-medium text-gray-900 dark:text-gray-300">Full name</label>
                        <input
                            v-model="semester"
                            type="text"
                            class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5"
                            placeholder="Fullname"
                            required=""
                        />
                    </div>
                    </div>
                         <label class="block mb-2 text-sm font-medium text-gray-900 dark:text-gray-300">Full name</label>
                        <input
                            v-model="attendance_score"
                            type="number"
                            class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5"
                            placeholder="Fullname"
                            required=""
                        />
                    </div>
                </div>
              

            </div> -->
        </main>
    </div>
</template>

<script>
import axios from "axios";
import ThemifyIcon from "vue-themify-icons/ThemifyIcon.vue";
import { mapState } from "vuex";
import Loading from "vue-loading-overlay";
import "vue-loading-overlay/dist/vue-loading.css";
import DashboardMenu from "@/components/DashboardMenu.vue";

export default {
    components: { ThemifyIcon, Loading, DashboardMenu },
    data() {
        return {
            isLoading: false,
            attendance_score: 0,
            assignment: 0,
            mid_tern: 0,
            final_tern: 0,
            id_course: "",
            semester: "",
            id_student: "",
        };
    },
    methods: {
        resetState() {
            this.attendance_score = 0;
            this.assignment = 0;
            this.mid_tern = 0;
            this.final_tern = 0;
            this.id_course = "";
            this.semester = "";
            this.id_student = "";
        },
        async registerAccountHandler() {
            this.isLoading = true;
            await axios
                .post(`${process.env.VUE_APP_API_GATEWAY}/user-service/v1/user/new`, {
                    fullName: this.fullName,
                    gender: this.gender,
                    id_faculty: this.id_faculty,
                    role: this.role,
                    address: this.address,
                    phoneNumber: this.phone,
                })
                .then((res) => {
                    if (res.data.status) {
                        this.toastify.success(res.data.message);
                        this.resetState();
                    } else {
                        this.toastify.error(res.data.message);
                    }
                })
                .catch((err) => {
                    if (!err.response?.data.message) return this.toastify.error(err.message);
                    this.toastify.error(err.response.data.message);
                });
            this.isLoading = false;
        },
    },
    computed: { ...mapState(["accessToken", "payload", "toastify"]) },
};
</script>
