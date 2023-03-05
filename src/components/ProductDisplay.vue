<template>
    <div class="main-container">
        <div v-if="setLoading === false" class="main-container" :class="dataMenWomen === false ? 'background-gray' : productAPI.dataProduct.category === 'men\'s clothing' ? 'background-aqua' : 'background-light-pink'">
            <div class="decoration-box">
                <img src="@/assets/decor.svg" alt="decoration" class="img-decor">
            </div>
            <div class="box-product">
                <div v-if="dataMenWomen === true" class="product-available-container">
                    <div class="product-image-box">
                        <img :src="productAPI.dataProduct.image" alt="product image" class="img-product">
                    </div>
                    <div class="product-part-box">
                        <div class="header">
                            <h1 class="product-title" :class="productAPI.dataProduct.category === 'men\'s clothing' ? 'font-navy' : 'font-purple'">{{ productAPI.dataProduct.title }}</h1>
                            <div class="product-category">
                                <span>{{ productAPI.dataProduct.category }}</span>
                                <div class="product-rate">
                                    <p>{{ productAPI.dataProduct.rating.rate }}/5</p>
                                    <span class="circle" :class="productAPI.dataProduct.category === 'men\'s clothing' ? 'background-navy' : 'background-purple'"></span>
                                    <span class="circle" :class="productAPI.dataProduct.category === 'women\'s clothing' ? 'background-purple' : 'background-navy'"></span>
                                    <span class="circle" :class="productAPI.dataProduct.category === 'men\'s clothing' ? 'background-navy' : 'background-purple'"></span>
                                    <span class="circle" :class="productAPI.dataProduct.category === 'women\'s clothing' ? 'background-purple' : 'background-navy'"></span>
                                    <span class="circle" :class="productAPI.dataProduct.category === 'men\'s clothing' ? 'background-navy' : 'background-purple'"></span>
                                </div>
                            </div>
                            <div class="product-desc">
                                <p>{{ productAPI.dataProduct.description }}</p>
                            </div>
                        </div>
                        <div class="footer">
                            <span class="product-price font-navy" :class="productAPI.dataProduct.category === 'men\'s clothing' ? 'font-navy' : 'font-purple'">${{ productAPI.dataProduct.price }}</span>
                            <div class="button-box">
                                <button class="button-buy" :class="productAPI.dataProduct.category === 'men\'s clothing' ? 'background-navy' : 'background-purple'" @click="buyButton()">Buy Now</button>
                                <button class="button-next" :class="productAPI.dataProduct.category === 'men\'s clothing' ? 'font-navy border-navy' : 'font-purple border-purple'" @click="getProduct()">Next Product</button>
                            </div>
                        </div>
                    </div>
                </div>
                <div v-else class="product-unavailable-container">
                    <div class="sad-face-box">
                        <img src="@/assets/sad-face.svg" alt="sad face" class="img-sad">
                    </div>
                    <div class="product-unavailable-box">
                        <p>This product is unavailable to show</p>
                    </div>
                    <div class="button-unv-box">
                        <button class="button-unv-next" @click="getProduct()">Next Product</button>
                    </div>
                </div>
            </div>
        </div>
        <div v-else class="box-loader">
            <div class="loader"></div>
        </div>
    </div>
</template>

<script>
export default {
    name: "ProductDisplay",
    data() {
        return {
            dataIndex: 0,
            setLoading: false,
            productAPI: {},
            dataMenWomen: false,
        };
    },

    methods: {
        async getDataFromAPI() {
            const api = await fetch(`https://fakestoreapi.com/products/${this.dataIndex}`);
            const response = await api.json();
            console.log(response);
            return response;
        },

        async getProduct() {
            this.setLoading = true;
            
            if (this.dataIndex !== 20) {
                this.dataIndex ++
            } else {
                this.dataIndex = 1;
            }

            let dataProduct = await this.getDataFromAPI()
            if (dataProduct.category === "men's clothing" || dataProduct.category === "women's clothing") {
                this.dataMenWomen = true;
                this.productAPI = { dataProduct }
            } else {
                this.dataMenWomen = false;
            }

            this.setLoading = false
            // console.log('INI GET PRODUCT');
            // console.log(dataProduct.description);
            // console.log(dataProduct.image);
        },
        
        async getTes() {
            console.log('TES SAJA');
        },

        buyButton() {
            alert('Sorry this feature is not yet available');
        }
    },

    mounted() {
        // console.log('Mounted')
        // this.getTes()
        // this.getDataFromAPI()
        this.getProduct();
    },

    // beforeMount() {
    //     console.log('Before Mount');
    // }

}
</script>

<style>
    @import "@/assets/style/page.css";
</style>