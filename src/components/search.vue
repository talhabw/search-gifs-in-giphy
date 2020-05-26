<template>
    <div class="search container">
        <div class="row">
            <div class="col-6 mt-3 offset-3 text-center">
                <div class="form-group">
                    <input
                        v-model="query"
                        @keypress.enter="handleSearch"
                        type="text"
                        class="form-control"
                        placeholder="Write the name of the gif"
                    />
                </div>
                <div class="col-12 p-0 text-right">
                    <button class="btn btn-primary" @click="handleSearch">Submit</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            query: ""
        };
    },
    methods: {
        handleSearch() {
            this.$emit("searchRequested", this.query);
        }
    }
};
</script>