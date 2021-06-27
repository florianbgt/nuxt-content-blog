<template>
    <article>
        <img v-if="'image' in article" :src="require(`~/content${$route.path}/${article.image}`)" style="width: 100%; height: 250px; object-fit: cover"/>
        <img v-else :src="require('~/content/blog/default.png')" style="width: 100%; height: 250px; object-fit: cover"/>
        <h1>{{ article.title }}</h1>
        <h4 class="text-secondary">
            <small>
                <i>
                    {{ new Date(article.createdAt).toLocaleDateString('en', { year: 'numeric', month: 'long', day: 'numeric' }) }}
                </i>
            </small>
        </h4>
        <nuxt-content :document="article" />
    </article>
</template>

<script>
export default {
    layout: 'blog',

    async asyncData({ $content, params }) {
        const article = await $content('blog', params.slug, 'index').fetch();
        return { article }
    }
}
</script>