<script>
    import { Input } from "$lib/components/ui/input/index";
    import { Button } from "$lib/components/ui/button/index";
    import { Label } from "$lib/components/ui/label/index";
    import * as Card from "$lib/components/ui/card/index";

    let { email='', handleSubmit = ((e) => { e.preventDefault() ; console.log('Submit!!') ; window.location.href = '/dashboard'}) } = $props();
</script>

<div class="flex flex-row items-center justify-center h-screen">
    <Card.Root class="w-[400px]">
        <Card.Header>
            <Card.Title class="text-2xl">Login</Card.Title>
            <Card.Description>
                Enter your email below to login to your account
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
                        <div class="flex items-center">
                            <Label for="password">Password</Label>
                            <a
                                href="/auth/reset"
                                class="ml-auto inline-block text-sm underline-offset-4 hover:underline"
                            >
                                Forgot your password?
                            </a>
                        </div>
                        <Input type="password" />
                    </div>

                    <div class="my-6">
                        <Button class="w-full" type="submit">Login</Button>
                    </div>
                </div>
            </form>
        </Card.Content>
    </Card.Root>
</div>
