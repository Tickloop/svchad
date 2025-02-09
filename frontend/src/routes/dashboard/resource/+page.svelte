<script>
    import DataTable from "$lib/components/data-table.svelte";
    import { Button, buttonVariants } from "$lib/components/ui/button/index";
    import * as Card from "$lib/components/ui/card/index";
    import Plus from "lucide-svelte/icons/plus";

    const columns = [
        {
            accessorKey: "status",
            header: "Status",
        },
        {
            accessorKey: "email",
            header: "Email",
        },
        {
            accessorKey: "amount",
            header: "Amount",
        },
    ];

    let data = [];
    for (let i = 0; i < 1000; i++) {
        data.push({
            status: "Active",
            email: "me@example.com",
            amount: 1000 + i,
        });
    }
</script>

<div class="p-4 mt-4">
    <div class="flex flex-row justify-between items-baseline gap-4">
        <h1 class="text-3xl">Resource</h1>
        <a href="/dashboard/resource/create" class={buttonVariants({ variant: 'outline' })}>
            <Plus />
            Add
        </a>
    </div>
    <div class="mt-4 pt-4">
        <DataTable {data} {columns} />
    </div>
</div>
