<script lang="ts">
    const components = [{ name: 'BlueThing' }, { name: 'GreenThing' }];
    
        const loadComponent = async (name: string) => {
            return (await import(`./${name}.svelte`)).default;
        };
    
    </script>


{#each components as component}
	{#await loadComponent(component.name) then myComponent}
		<svelte:component this={myComponent} />
	{/await}
{/each}