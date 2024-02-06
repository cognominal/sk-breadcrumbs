<script context="module">
    export const ssr = false
</script>

<script lang="ts">
	import '../app.postcss';
	import { AppShell, AppBar } from '@skeletonlabs/skeleton';
	import YAML from 'yaml'
    import { Pane, Splitpanes } from 'svelte-splitpanes';

</script>

<ol class="breadcrumb">
	<li class="crumb"><a class="anchor" href="/elements/breadcrumbs">Skeleton</a></li>
	<li class="crumb-separator" aria-hidden>&rsaquo;</li>
	<li class="crumb"><a class="anchor" href="/elements/breadcrumbs">Elements</a></li>
	<li class="crumb-separator" aria-hidden>&rsaquo;</li>
	<li>Breadcrumbs</li>
</ol>


<Splitpanes class="text-black">
	<Pane minSize={20}>1<br /><em class="specs">I have a min width of 20%</em></Pane>
	<Pane>5</Pane>
</Splitpanes>