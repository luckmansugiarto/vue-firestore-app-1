<template>
    <div>
        <add-product 
            v-bind:product="product"
            v-bind:onAdd="onAdd"
        />

        <product-list
            v-bind:editedProduct="editedProduct"
            v-bind:sortedProducts="sortedProducts"
            v-bind:onCancel="onCancel"
            v-bind:onDelete="onDelete"
            v-bind:onEdit="onEdit"
            v-bind:onSave="onSave"
        />
    </div>
</template>

<script>
import db from '@/db'
import AddProduct from './AddProduct'
import ProductList from './ProductList'

export default {
    name: 'Products',
    data () {
        return {
            editedProduct: {},
            product: {
                product_id: '',
                name: '',
                price: ''
            },
            products: []
        }
    },
    components: {
        AddProduct,
        ProductList
    },
    computed: {
        sortedProducts () {
            return this.products.slice().sort((a, b) => {
                return parseInt(a.product_id) > parseInt(b.product_id)
            })
        }
    },
    created () {
        this.getProducts()
    },
    methods: {
        getProducts() {
            this.products = []
            db.collection('Products').get()
                .then(querySnapshot => {
                    querySnapshot.forEach(doc => {
                        this.products.push(doc.data())
                    })
                })
        },
        onAdd () {
            db.collection('Products').add(this.product)
                .then(this.getProducts())
        },
        onCancel () {
            this.editedProduct = {}
        },
        onDelete (product_id) {
            db.collection('Products')
                .where('product_id', '==', product_id)
                .get()
                .then(querySnapshot => {
                    querySnapshot.forEach(doc => {
                        doc.ref.delete().then(this.getProducts())
                    })
                })
        },
        onEdit (product) {
            this.editedProduct = JSON.parse(JSON.stringify(product))
        },
        onSave () {
            db.collection('Products')
                .where('product_id', '==', this.editedProduct.product_id)
                .get()
                .then(querySnapshot => {
                    querySnapshot.forEach(doc => {
                        doc.ref.set(this.editedProduct).then(() => {
                            this.getProducts()
                            this.onCancel()
                        })
                    })
                })
        }
    }
}
</script>