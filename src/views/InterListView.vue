<template>
    <div>
        <p v-for="(u,i) in data.boardList" :key="i">{{u}}</p>
    </div>
</template>

<script>
import { onMounted, reactive } from 'vue';
import axios from 'axios';

export default {
    name: 'InterListView',
    setup() {
        const data = reactive({
            boardList: []
        });
        const getList = () => {
            axios.get('http://localhost:8090/api/list')
                .then(function (response) {
                    data.boardList = response.data;
                    console.log(data.boardList);
                })
                .catch(function (error) {
                    console.log(error);
                });
        };
        onMounted(() => {
            getList();
        })
        return {
            data,
            getList
        }
    }
};
</script>