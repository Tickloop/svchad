<script>
    import DataTable from "$lib/components/data-table.svelte";
    import { Button } from "$lib/components/ui/button/index";
    import * as Card from "$lib/components/ui/card/index";
    import Plus from "lucide-svelte/icons/plus";

    import Add from "$lib/components/add-resource.svelte";

    // add logic to fetch the resource record and pass into Add below
</script>

<div class="p-4 mt-4">
    <div class="flex flex-row justify-between items-baseline gap-4">
        <h1 class="text-3xl">Resource</h1>
    </div>

    <Add />
</div>
