<template>
    <div>
        <h3>Add Product</h3>
        <div class="card products__add-product">
            <div>
                <input v-model="product.product_id" type="text" class="validate" placeholder="id"/>
            </div>
            <div>
                <input v-model="product.name" type="text" class="validate" placeholder="name"/>
            </div>
            <div>
                <input v-model="product.price" type="text" class="validate" placeholder="price"/>
            </div>
            <div>
                <i class="material-icons medium" @click="onAdd">
                    add
                </i>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'AddProduct',
    props: [
        'product',
        'onAdd'
    ]
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.products__add-product {
    align-item: center;
    display: flex;
    justify-content: space-between;
}
</style>
