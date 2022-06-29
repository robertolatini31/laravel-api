<template>
    <div>
        <h1 class="text-center py-5">Work In Progress</h1>

        <section class="posts">
            <div class="container">
                <div class="row row-cols-1 row-cols-sm-2 row-cols-md-3">
                    <div class="col" v-for="post in postsResponse.data" :key="post.id">
                        <div class="product card">
                            <img :src="post.img" :alt="post.title">
                            <div class="card-body">
                                <h3>{{post.title}}</h3>
                                <p>{{post.content}}</p>
                            </div>
                            <div class="card-footer">
                                <span v-if="post.category"><strong>Categoria: </strong>{{ post.category.name}}</span>
                                <div class="tags" v-if="post.tags.length > 0">
                                    <ul>
                                        <strong>Tags:</strong>
                                        <li v-for="tag in post.tags" :key="tag.id">
                                            {{tag.name}}
                                        </li>
                                    </ul>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </section>
    </div>
</template>

<script>
export default {
    name: 'App',
    components:{},
    data() {
        return {
            posts: '',
            postsResponse: '',
        }
    },
    methods: {
        getAllPosts(){
            axios.get('/api/posts').then((response => {
                this.postsResponse = response.data;
            })).catch(e => {
                console.log(e);
            })
        }
    },
    mounted() {
       this.getAllPosts();
    }
}
</script>