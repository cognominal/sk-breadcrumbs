<script lang="ts">
	import '../app.postcss';
	import { AppShell, AppBar } from '@skeletonlabs/skeleton';
	import YAML from 'yaml'

const parsed = "-0"
const yamls =`	
TOP/statementlist : { from: 0, to: 2}
a :
  - statement: { from: 0, to: 2}
    h :
       EXPR/value/number :  { from: 0, to: 2}
       h :
         sign : { from: 0, to: 1}
         integer/VALUE : { from: 1, to: 2}
`
const data = YAML.parse(yamls)

</script>

<ol class="breadcrumb">
	<li class="crumb"><a class="anchor" href="/elements/breadcrumbs">Skeleton</a></li>
	<li class="crumb-separator" aria-hidden>&rsaquo;</li>
	<li class="crumb"><a class="anchor" href="/elements/breadcrumbs">Elements</a></li>
	<li class="crumb-separator" aria-hidden>&rsaquo;</li>
	<li>Breadcrumbs</li>
</ol>