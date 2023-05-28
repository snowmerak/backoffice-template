<script>
    import Router, {push} from "svelte-spa-router";

    import {Button, TreeView} from "carbon-components-svelte";
    import {OpenPanelFilledLeft} from "carbon-icons-svelte";
    import Counter from "./lib/page/Counter.svelte";
    import Index from "./lib/page/Index.svelte";
    import Login from "./lib/page/Login.svelte";

    let openSidebar = false;
    let activeId = "/";
    let selectedIds = [];
    let children = [
        { id: "/", text: "Index Page" },
        { id: "/login", text: "Login Page" },
        { id: "/counter", text: "Counter Page" },
    ];

    const routes = {
        "/": Index,
        "/login": Login,
        "/counter": Counter,
    };

    const onRouteChange = (id) => {
        if (id !== "" && id !== undefined && id !== null) {
            push(id);
        }
    };

    $: onRouteChange(activeId);
</script>

<div class="grid">
    <div class="header">
        <div class="row">
            <h1>Back Office</h1>
            <div class="drawer-button">
                <input id="drawer-toggle" type="checkbox" class="hidden" bind:checked={openSidebar} />
                <Button kind="ghost" icon={OpenPanelFilledLeft} iconDescription="Open Menu" on:click={() => openSidebar = !openSidebar}></Button>
            </div>
        </div>
    </div>
    <div class="sidebar drawer" class:closed_drawer={!openSidebar} class:opened_drawer={openSidebar}>
        <div class="drawer-button">
            <Button kind="ghost" icon={OpenPanelFilledLeft} iconDescription="Open Menu" on:click={() => openSidebar = !openSidebar}></Button>
        </div>
        <TreeView
                labelText="Menu"
                {children}
                bind:activeId
                bind:selectedIds
        />
    </div>
    <div class="main">
        <Router {routes} />
    </div>
</div>

