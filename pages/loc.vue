<!-- <script>
export default {
    data() {
        return {
            showFavorites: false,
            favoriteList: [
                { id: 1, name: 'Sản phẩm 1' },
                { id: 2, name: 'Sản phẩm 2' },
                { id: 3, name: 'Sản phẩm 3' },
                { id: 4, name: 'Sản phẩm 4' },
                { id: 5, name: 'Sản phẩm 5' },
            ],
        };
    },
};
</script>



<template>
    <div>
        <button @click="showFavorites = !showFavorites">
            {{ showFavorites ? 'Ẩn Danh Sách Yêu Thích' : 'Hiện Danh Sách Yêu Thích' }}
        </button>
        <ul v-if="showFavorites">
            <li v-for="item in favoriteList" :key="item.id">
                {{ item.name }}
            </li>
        </ul>
    </div>
</template> -->
<template>
    <div>
        <button @click="toggleVisibility">
            {{ isVisible ? 'Ẩn' : 'Hiện' }} nội dung
        </button>
        <p v-if="isVisible">Nội dung được hiển thị</p>
    </div>
</template>

<script>
export default {
    data() {
        return {
            isVisible: false,
        };
    },
    methods: {
        toggleVisibility() {
            this.isVisible = !this.isVisible;
        },
    },
};
</script>