How to programmatically import components, and render them.

The trick for me was to wrap `await import()` inside brackets, and extract the `default` object:
``` .js
return (await import(`./${name}.svelte`)).default;
```

This would fail if the thing you're importing is not a component, so you can try and wrap it in a try statement or something. But for proof of concept, this worked perfectly.

Full code:
``` .svelte
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
```