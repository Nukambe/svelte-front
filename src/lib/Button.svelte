<script>
    export let size = "small";
    export let shadow = false;
    export let type;
    export let disabled = false;
</script>

<button
    class:size-lg={size === "large"}
    class:size-sm={size === "small"}
    class:shadow
    style:background-color={"red"}
    {type}
    {disabled}
>
    {#if $$slots.leftcontent}
        <div class="left-content">
            <slot name="leftcontent" />
        </div>
    {/if}
    <slot>fallback</slot>
</button>

<style>
    button {
        display: flex;
        align-items: center;
    }
    .left-content {
        margin-right: 10px;
        width: 40px;
    }
    .size-sm {
        padding: 0px;
    }

    .size-lg {
        padding: 16px;
    }

    .shadow {
        box-shadow: 0 0 10px black;
    }
</style>
