<template>
    <div>
        <h3 class="text-center">Edit Post</h3>
        <div class="row">
            <div class="col-md-6">
                <form @submit.prevent="updatePost">
                    <div class="form-group">
                        <label>Title</label>
                        <input type="text" class="form-control" v-model="post.title">
                    </div>
                    <div class="form-group">
                        <label>Description</label>
                        <input type="text" class="form-control" v-model="post.description">
                    </div>
                    <div class="form-group">
                        <label>Attachment</label>
                        <input type="text" class="form-control" v-model="post.attachment">
                    </div>
                    <div class="form-group">
                        <label>Departement</label>
                        <input type="text" class="form-control" v-model="post.departement">
                    </div>
                    <div class="form-group">
                        <label>Assign</label>
                        <input type="text" class="form-control" v-model="post.assign">
                    </div>
                    <div class="form-group">
                        <label>CC</label>
                        <input type="text" class="form-control" v-model="post.cc">
                    </div>
                    <button type="submit" class="btn btn-primary">Update Post</button>
                </form>
            </div>
        </div>
    </div>
</template>
  
<script>
    export default {
        data() {
            return {
                post: {}
            }
        },
        created() {
            this.axios
                .get(`http://127.0.0.1:8000/api/post/edit/${this.$route.params.id}`)
                .then((response) => {
                    this.post = response.data;
                    // console.log(response.data);
                });
        },
        methods: {
            updatePost() {
                this.axios
                    .post(`http://127.0.0.1:8000/api/post/update/${this.$route.params.id}`, this.post)
                    .then((response) => {
                        this.$router.push({name: 'home'});
                    });
            }
        }
    }
</script>