<template>
	<div>
		<h3>Products</h3>
        <div v-for="product in sortedProducts" class="collection">
            <div
                v-if="product.product_id === editedProduct.product_id"
                class="collection-item products__list-item"
                :class="{ 'yellow lighten-4': editedProduct.product_id === product.product_id }"
            >
                <div>{{ product.product_id }}</div>
                <div>
                    <input v-model="editedProduct.name" type="text" class="validate" placeholder="name"/>
                </div>
                <div>
                    <input v-model="editedProduct.price" type="text" class="validate" placeholder="price"/>
                </div>
                <div>
                    <i class="material-icons" @click="onSave()">
                        check
                    </i>
                    <i class="material-icons" @click="onCancel()">
                        cancel
                    </i>
                </div>
            </div>
            <div v-else class="collection-item products__list-item">
                <div>{{ product.product_id }}</div>
                <div>{{ product.name }}</div>
                <div>{{ product.price }}</div>
                <div>
                    <i class="material-icons" @click="onEdit(product)">
                        mode_edit
                    </i>
                    <i class="material-icons" @click="onDelete(product.product_id)">
                        delete
                    </i>
                    <router-link
                        :to="{
                            name: 'ProductPage',
                            params: {
                                product_id: product.product_id
                            }
                        }"
                    >
                        <i class="material-icons">
                            search
                        </i>
                    </router-link>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'ProductList',
    props: [
    	'editedProduct',
        'sortedProducts',
        'onCancel',
        'onDelete',
        'onEdit',
        'onSave'
    ]
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.products__list-item {
    align-item: center;
    display: flex;
    justify-content: space-between;
}
</style>
