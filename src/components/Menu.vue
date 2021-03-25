<template>
    <div>
        <b-dropdown id="dropdown-1" size="sm" text="Select Category:" class="m-md-2">
            <b-dropdown-item
                v-for="api in apis"
                :key="api.id"
                :value="api.api"
                @click="chooseApi(api.api, api.name)"
            >
                {{ api.name }}
            </b-dropdown-item>
        </b-dropdown>
    </div>
</template>
<script>
export default {
    props: {
        fetchApi: Function
    },
    data() {
        return {
            apis: [
                {
                    id: 1,
                    name: 'Any Category',
                    api: 'https://opentdb.com/api.php?amount=10&type=multiple'
                },
                {
                    id: 20,
                    name: 'Mythology',
                    api: 'https://opentdb.com/api.php?amount=10&category=20&type=multiple'
                },
                {
                    id: 26,
                    name: 'Celebrities',
                    api: 'https://opentdb.com/api.php?amount=10&category=26&type=multiple'
                },
                {
                    id: 21,
                    name: 'Sports',
                    api: 'https://opentdb.com/api.php?amount=10&category=21&type=multiple'
                },
                {
                    id: 18,
                    name: 'Computers',
                    api: 'https://opentdb.com/api.php?amount=10&category=18&type=multiple'
                },
                {
                    id: 11,
                    name: 'Film',
                    api: 'https://opentdb.com/api.php?amount=10&category=11&type=multiple'
                },
                {
                    id: 10,
                    name: 'Books',
                    api: 'https://opentdb.com/api.php?amount=10&category=10&type=multiple'
                },
                {
                    id: 23,
                    name: 'History',
                    api: 'https://opentdb.com/api.php?amount=10&category=23&type=multiple'
                },
            ]
        }
    },
    methods: {
        chooseApi(value, name) {
            this.fetchApi(value, name);
            this.$emit('resetMenu');
        }
    },
}
</script>
<style scoped>
div {
  position: relative;
  z-index: 1;
  padding-top: 15px;
  padding-bottom: 10px;
  border-bottom-left-radius: 4px;
  border-bottom-right-radius: 4px;
  background-color: #e9ecef;
}

.dropdown-item {
  font-size: 14px !important;
}

.dropdown-item:hover, .dropdown-item:focus {
  background-color: turquoise !important;
}

</style>