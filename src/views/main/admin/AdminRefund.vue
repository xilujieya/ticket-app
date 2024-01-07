<template>
    <div class="order">
        <RefundList></RefundList>
        <RefundPagination></RefundPagination>
    </div>
</template>
  
<script>
import RefundPagination from './refund/RefundPagination.vue';
import RefundList from './refund/RefundList.vue';

export default {
    components: {
        RefundPagination,
        RefundList
    },
    data() {
        return {}
    },
}
</script>
  
<style>
.order {
    width: 1200px;
    margin: 0 auto;
    padding-top: 15px;
}
</style>