<script context="module">
    import { gql } from 'graphql-request'
    import { client } from '$lib/graphql-client'
    import  ProjectCard from '$lib/components/project-card.svelte' 

    export const load = async () => {
        const query = gql`
            query GetProjects {
                projects {
                    name
                    slug
                    description
                    demo
                    sourceCode
                    image {
                        url
                    }
                }
            }
        `
        const { projects } = await client.request(query)

        return { props: { projects } }
    }
</script>

<script>
    export let projects
</script>

{#each projects as {image, name, slug, description}}
    <ProjectCard {name} {description} url={image[0].url} {slug} />    
{/each}