<script>
    import {
        getCoreRowModel,
        getPaginationRowModel,
    } from "@tanstack/table-core";
    import {
        createSvelteTable,
        FlexRender,
    } from "$lib/components/ui/data-table/index.js";
    import * as Table from "$lib/components/ui/table/index.js";
    import { Button } from "$lib/components/ui/button/index";
    import ChevronRight from "lucide-svelte/icons/chevron-right";
    import ChevronsRight from "lucide-svelte/icons/chevrons-right";
    import ChevronLeft from "lucide-svelte/icons/chevron-left";
    import ChevronsLeft from "lucide-svelte/icons/chevrons-left";
    import * as Select from "$lib/components/ui/select/index";


    let { data, columns } = $props();
    let pagination = $state({ pageIndex: 0, pageSize: 10 });
    let hasPreviousPage = false;
    let hasNextPage = true;

    const table = createSvelteTable({
        get data() {
            return data;
        },
        columns,
        getCoreRowModel: getCoreRowModel(),
        getPaginationRowModel: getPaginationRowModel(),
        
        state: {
            get pagination() {
                return pagination;
            },
        },
        onPaginationChange: (updater) => {
            if (typeof updater === "function") {
                pagination = updater(pagination);
            } else {
                pagination = updater;
            }
        },
    });
</script>

<div class="rounded-md border">
    <Table.Root>
        <Table.Header>
            {#each table.getHeaderGroups() as headerGroup (headerGroup.id)}
                <Table.Row>
                    {#each headerGroup.headers as header (header.id)}
                        <Table.Head>
                            {#if !header.isPlaceholder}
                                <FlexRender
                                    content={header.column.columnDef.header}
                                    context={header.getContext()}
                                />
                            {/if}
                        </Table.Head>
                    {/each}
                </Table.Row>
            {/each}
        </Table.Header>
        <Table.Body>
            {#each table.getRowModel().rows as row (row.id)}
                <Table.Row data-state={row.getIsSelected() && "selected"}>
                    {#each row.getVisibleCells() as cell (cell.id)}
                        <Table.Cell>
                            <FlexRender
                                content={cell.column.columnDef.cell}
                                context={cell.getContext()}
                            />
                        </Table.Cell>
                    {/each}
                </Table.Row>
            {:else}
                <Table.Row>
                    <Table.Cell
                        colspan={columns.length}
                        class="h-24 text-center"
                    >
                        No results.
                    </Table.Cell>
                </Table.Row>
            {/each}
        </Table.Body>
    </Table.Root>
</div>


<!-- pagination -->
<div class="flex m-2 p-2 items-center justify-end gap-2">
    <!-- rows per page -->
    <div class="flex items-center gap-2">
        <p class="hidden lg:block text-sm font-medium">Rows per page</p>
        <Select.Root
            type="single"
            onValueChange={(value) => {
                table.setPageSize(Number(value))
            }}
        >
            <Select.Trigger class="h-8 w-[70px]">
                {table.getState().pagination.pageSize}
            </Select.Trigger>
            <Select.Content>
                {#each [10, 20, 50, 100] as value}
                    <Select.Item value={value}>{value}</Select.Item>
                {/each}
            </Select.Content>
        </Select.Root>
    </div>

    <!-- navigate pages -->
    <div class="flex items-center space-x-2">
        <Button
            variant="outline"
            class="h-8 w-8 p-0 lg:flex"
            onclick={() => { table.firstPage() }}
            disabled={!table.getCanPreviousPage()}
        >
            <span class="sr-only">Go to first page</span>
            <ChevronsLeft size={15} />
        </Button>
        <Button
            variant="outline"
            class="h-8 w-8 p-0"
            onclick={() => { table.previousPage() }}
            disabled={!table.getCanPreviousPage()}
        >
            <span class="sr-only">Go to previous page</span>
            <ChevronLeft size={15} />
        </Button>
        <span class="text-sm font-medium">Page {pagination.pageIndex + 1} of {table.getPageCount()}</span>
        <Button
            variant="outline"
            class="h-8 w-8 p-0"
            disabled={!table.getCanNextPage()}
            onclick={() => { table.nextPage() }}
        >
            <span class="sr-only">Go to next page</span>
            <ChevronRight size={15} />
        </Button>
        <Button
            variant="outline"
            class="h-8 w-8 p-0 lg:flex"
            disabled={!table.getCanNextPage()}
            onclick={() => { table.lastPage() }}
        >
            <span class="sr-only">Go to last page</span>
            <ChevronsRight size={15} />
        </Button>
    </div>
</div>
