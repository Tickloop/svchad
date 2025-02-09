<script>
    import { Input } from "$lib/components/ui/input/index";
    import { Button } from "$lib/components/ui/button/index";
    import { Label } from "$lib/components/ui/label/index";
    import * as Card from "$lib/components/ui/card/index";

    let { email='', handleSubmit = ((e) => { e.preventDefault() ; window.location.href = '/dashboard/resource'}) } = $props();
</script>

<div class="mt-2 pt-2 flex flex-row items-center">
    <Card.Root class="w-[400px]">
        <Card.Header>
            <Card.Title class="text-2xl">Create Resource</Card.Title>
            <Card.Description>
                Enter the details to create a new resource
            </Card.Description>
        </Card.Header>
        <Card.Content>
            <form onsubmit={handleSubmit}>
                <div class="flex flex-col gap-6">
                    <div class="grid gap-2">
                        <Label for="email">Email</Label>
                        <Input
                            type="email"
                            id="email"
                            placeholder="me@example.com"
                            bind:value={email}
                        />
                    </div>

                    <div class="grid gap-2">
                        <Label for="Amount">Amount</Label>
                        <Input type="number" />
                    </div>

                    <div class="my-6">
                        <Button class="w-full" type="submit" variant="outline">Create</Button>
                    </div>
                </div>
            </form>
        </Card.Content>
    </Card.Root>
</div>
