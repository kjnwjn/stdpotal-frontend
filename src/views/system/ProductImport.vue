<template>
    <div>
        <DashboardMenu />
        <main class="main-container">
            <Loading :active="isLoading" :is-full-page="true" :can-cancel="false" />
            <div class="mb-20">
                <div class="flex items-center mb-4 text-green-700 font-bold text-lg uppercase">
                    <ThemifyIcon icon="menu" />
                    <h1 class="ml-2">Products management</h1>
                </div>
                <div class="mb-6">
                    <div class="mb-2 text-md font-medium text-gray-900 flex items-center">
                        <ThemifyIcon icon="settings" />
                        <p class="ml-2">Import products list from excel:</p>
                    </div>
                    <div class="flex mb-6">
                        <input
                            v-on:change="uploadFile('product')"
                            ref="file"
                            class="block w-full text-sm text-gray-900 bg-gray-50 rounded-lg border border-gray-300 cursor-pointer pl-2 py-2 mr-4"
                            type="file"
                        />
                        <div
                            v-on:click="importExcelHandler('product')"
                            class="flex justify-center items-center transition-all bg-blue-400 hover:bg-blue-500 text-white w-80 text-center rounded cursor-pointer"
                        >
                            <ThemifyIcon icon="upload" />
                            <button class="ml-2">Import</button>
                        </div>
                    </div>
                    <div class="mb-2 text-md font-medium text-gray-900 flex items-center">
                        <ThemifyIcon icon="settings" />
                        <p class="ml-2">Download file format of excel to import products:</p>
                    </div>
                    <div
                        v-on:click="downloadExampleHandler('product')"
                        class="flex justify-center items-center transition-all bg-green-400 hover:bg-green-500 text-white w-60 py-2 rounded mb-4 cursor-pointer"
                    >
                        <ThemifyIcon icon="download" />
                        <button class="ml-2">Donwload example</button>
                    </div>
                </div>

                <div class="mb-2 text-md font-medium text-gray-900 flex items-center">
                    <ThemifyIcon icon="settings" />
                    <p class="ml-2">Insert new product manually:</p>
                </div>
                <div class="grid gap-6 mb-6 md:grid-cols-2">
                    <div>
                        <label class="block mb-2 text-sm font-medium text-gray-900 dark:text-gray-300">Barcode</label>
                        <input
                            type="text"
                            v-model="barcode"
                            class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5"
                            placeholder="Product barcode"
                            required=""
                        />
                    </div>
                    <div>
                        <label class="block mb-2 text-sm font-medium text-gray-900 dark:text-gray-300">Product name</label>
                        <input
                            type="text"
                            v-model="productName"
                            class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5"
                            placeholder="Product name"
                            required=""
                        />
                    </div>
                    <div>
                        <label class="block mb-2 text-sm font-medium text-gray-900 dark:text-gray-300">UOM (Unit of Measure)</label>
                        <input
                            type="email"
                            v-model="uom"
                            class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5"
                            placeholder="GOI/HOP/TUI..."
                            required=""
                        />
                    </div>
                    <div>
                        <label class="block mb-2 text-sm font-medium text-gray-900 dark:text-gray-300">Department</label>
                        <input
                            type="text"
                            v-model="department"
                            class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5"
                            placeholder="CHIPS & SNACKS"
                            required=""
                        />
                    </div>
                    <div>
                        <label class="block mb-2 text-sm font-medium text-gray-900 dark:text-gray-300">Supplier code</label>
                        <input
                            type="text"
                            v-model="supplierCode"
                            class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5"
                            placeholder="Supplier code"
                            required=""
                        />
                    </div>
                    <div>
                        <label class="block mb-2 text-sm font-medium text-gray-900 dark:text-gray-300">Unit cost</label>
                        <input
                            type="number"
                            v-model="unitCost"
                            class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5"
                            placeholder="1000"
                            required=""
                        />
                    </div>
                </div>
                <div class="mb-6">
                    <label class="block mb-2 text-sm font-medium text-gray-900 dark:text-gray-300">Quanity</label>
                    <input
                        type="number"
                        v-model="quantity"
                        class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5"
                        placeholder="100"
                        required=""
                    />
                </div>
                <button
                    type="submit"
                    v-on:click="registerProductHandler"
                    class="text-white transition-all bg-blue-400 hover:bg-blue-500 focus:outline-none font-medium rounded-lg text-sm w-full sm:w-auto px-9 py-2.5 text-center"
                >
                    Submit
                </button>
            </div>
            <div class="mb-20">
                <div class="flex items-center mb-4 text-green-700 font-bold text-lg uppercase">
                    <ThemifyIcon icon="menu" />
                    <h1 class="ml-2">Suppliers management</h1>
                </div>
                <div class="mb-6">
                    <div class="mb-2 text-md font-medium text-gray-900 flex items-center">
                        <ThemifyIcon icon="settings" />
                        <p class="ml-2">Import suppliers list from excel:</p>
                    </div>
                    <div class="flex mb-6">
                        <input
                            v-on:change="uploadFile('supplier')"
                            ref="file2"
                            class="block w-full text-sm text-gray-900 bg-gray-50 rounded-lg border border-gray-300 cursor-pointer pl-2 py-2 mr-4"
                            type="file"
                        />
                        <div
                            v-on:click="importExcelHandler('supplier')"
                            class="flex justify-center items-center transition-all bg-blue-400 hover:bg-blue-500 text-white w-80 text-center rounded cursor-pointer"
                        >
                            <ThemifyIcon icon="upload" />
                            <button class="ml-2">Import</button>
                        </div>
                    </div>
                    <div class="mb-2 text-md font-medium text-gray-900 flex items-center">
                        <ThemifyIcon icon="settings" />
                        <p class="ml-2">Download file format of excel to import supplier:</p>
                    </div>
                    <div
                        v-on:click="downloadExampleHandler('supplier')"
                        class="flex justify-center items-center transition-all bg-green-400 hover:bg-green-500 text-white w-60 py-2 rounded mb-4 cursor-pointer"
                    >
                        <ThemifyIcon icon="download" />
                        <button class="ml-2">Donwload example</button>
                    </div>
                </div>

                <div class="mb-2 text-md font-medium text-gray-900 flex items-center">
                    <ThemifyIcon icon="settings" />
                    <p class="ml-2">Insert new supplier manually:</p>
                </div>
                <div class="grid gap-6 mb-6 md:grid-cols-2">
                    <div>
                        <label class="block mb-2 text-sm font-medium text-gray-900 dark:text-gray-300">Supplier code</label>
                        <input
                            type="text"
                            v-model="supplier.supplierCode"
                            class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5"
                            placeholder="Supplier barcode"
                        />
                    </div>
                    <div>
                        <label class="block mb-2 text-sm font-medium text-gray-900 dark:text-gray-300">Supplier name</label>
                        <input
                            type="text"
                            v-model="supplier.supplierName"
                            class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5"
                            placeholder="Supplier name"
                        />
                    </div>
                </div>
                <div class="mb-6">
                    <label class="block mb-2 text-sm font-medium text-gray-900 dark:text-gray-300">Address</label>
                    <input
                        type="text"
                        v-model="supplier.supplierAdress"
                        class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5"
                        placeholder="Address"
                    />
                </div>
                <div class="mb-6">
                    <label class="block mb-2 text-sm font-medium text-gray-900 dark:text-gray-300">Phone number</label>
                    <input
                        v-model="supplier.supplierPhoneNumber"
                        type="tel"
                        class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5"
                        placeholder="0123-456-789"
                        pattern="[0-9]{4}-[0-9]{3}-[0-9]{3}"
                    />
                </div>
                <button
                    type="submit"
                    v-on:click="registerSupplierHandler"
                    class="text-white transition-all bg-blue-400 hover:bg-blue-500 focus:outline-none font-medium rounded-lg text-sm w-full sm:w-auto px-9 py-2.5 text-center"
                >
                    Submit
                </button>
            </div>
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
    data() {
        return {
            isLoading: false,
            barcode: null,
            productName: null,
            uom: null,
            department: null,
            supplierCode: null,
            unitCost: null,
            quantity: null,
            fileImport: null,
            supplier: {
                supplierCode: null,
                supplierName: null,
                supplierAdress: null,
                supplierPhoneNumber: null,
            },
        };
    },
    methods: {
        uploadFile(type = "product") {
            this.fileImport = type == "product" ? this.$refs.file.files[0] : this.$refs.file2.files[0];
        },
        async downloadExampleHandler(type = "product") {
            await axios({
                url: `${process.env.VUE_APP_API_GATEWAY}/${type == "product" ? "product" : "supplier"}/download-example?token=${this.accessToken}`,
                method: "GET",
                responseType: "blob",
            }).then((response) => {
                const fileURL = window.URL.createObjectURL(new Blob([response.data]));
                const fileLink = document.createElement("a");
                fileLink.href = fileURL;
                const fileName = `${type == "product" ? "product" : "supplier"}-example.xlsx`;
                fileLink.setAttribute("download", fileName);
                fileLink.setAttribute("target", "_blank");
                document.body.appendChild(fileLink);
                fileLink.click();
                fileLink.remove();
            });
        },
        async registerProductHandler() {
            this.isLoading = true;
            await axios
                .post(`${process.env.VUE_APP_API_GATEWAY}/product/register?token=${this.accessToken}`, {
                    barcode: this.barcode,
                    productName: this.productName,
                    UOM: this.uom,
                    department: this.department,
                    supplierCode: this.supplierCode,
                    unitCost: this.unitCost,
                    quantity: this.quantity,
                })
                .then((res) => {
                    if (res.data.status) {
                        this.toastify.success(res.data.msg.en);
                        this.barcode = null;
                        this.productName = null;
                        this.uom = null;
                        this.department = null;
                        this.supplierCode = null;
                        this.unitCost = null;
                        this.quantity = null;
                    } else {
                        this.toastify.error(res.data.msg.en);
                    }
                })
                .catch((err) => {
                    this.toastify.error(err.response.data.msg.en);
                });
            this.isLoading = false;
        },
        async registerSupplierHandler() {
            this.isLoading = true;
            await axios
                .post(`${process.env.VUE_APP_API_GATEWAY}/supplier/register?token=${this.accessToken}`, {
                    supplierCode: this.supplier.supplierCode,
                    supplierName: this.supplier.supplierName,
                    address: this.supplier.supplierAdress,
                    phoneNumber: this.supplier.supplierPhoneNumber,
                })
                .then((res) => {
                    if (res.data.status) {
                        this.toastify.success(res.data.msg.en);
                        this.supplier.supplierCode = null;
                        this.supplier.supplierName = null;
                        this.supplier.supplierAdress = null;
                        this.supplier.supplierPhoneNumber = null;
                    } else {
                        this.toastify.error(res.data.msg.en);
                    }
                })
                .catch((err) => {
                    this.toastify.error(err.response.data.msg.en);
                });
            this.isLoading = false;
        },
        async importExcelHandler(type = "product") {
            this.isLoading = true;
            const formData = new FormData();
            formData.append("file", this.fileImport);
            const headers = { "Content-Type": "multipart/form-data" };
            await axios
                .post(`${process.env.VUE_APP_API_GATEWAY}/${type == "product" ? "product" : "supplier"}/import?token=${this.accessToken}`, formData, { headers })
                .then((res) => {
                    console.log(res.data);
                    if (res.data.status) {
                        this.toastify.success(res.data.msg.en);
                    } else {
                        this.toastify.error(res.data.msg.en);
                    }
                })
                .catch((err) => {
                    this.toastify.error(err.response.data.msg.en);
                    console.log(err);
                });
            this.isLoading = false;
        },
    },
    components: { ThemifyIcon, Loading, DashboardMenu },
    computed: { ...mapState(["accessToken", "payload", "toastify"]) },
};
</script>
