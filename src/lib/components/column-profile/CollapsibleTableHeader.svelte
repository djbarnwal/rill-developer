<script lang="ts">
    import { createEventDispatcher } from "svelte";
    import { tick } from "svelte/internal";
    import { tweened } from "svelte/motion";
    import { cubicInOut as easing } from "svelte/easing";

    import { format } from "d3-format";

    import NavEntry from "$lib/components/column-profile/NavEntry.svelte";
    import ContextButton from "$lib/components/column-profile/ContextButton.svelte";

    import MoreIcon from "$lib/components/icons/MoreHorizontal.svelte";

    import Shortcut from "$lib/components/tooltip/Shortcut.svelte";
    import StackingWord from "$lib/components/tooltip/StackingWord.svelte";
    import TooltipShortcutContainer from "$lib/components/tooltip/TooltipShortcutContainer.svelte";
    import TooltipTitle from "$lib/components/tooltip/TooltipTitle.svelte";

    import { onClickOutside } from "$lib/util/on-click-outside";
    import { guidGenerator } from "$lib/util/guid";

    import notificationStore from "$lib/components/notifications/";

    export let name: string;
    export let cardinality: number;
    export let sizeInBytes: number = undefined;
    export let emphasizeTitle = false;
    export let menuX: number = undefined;
    export let menuY: number = undefined;
    export let show = false;
    export let contextMenuOpen = false;
    export let contextMenu: any;
    
    const dispatch = createEventDispatcher();

    const formatInteger = format(",");

    let cardinalityTween = tweened(cardinality, { duration: 600, easing });
    let sizeTween = tweened(sizeInBytes, { duration: 650, easing, delay: 150 });

    $: cardinalityTween.set(cardinality || 0);
    $: interimCardinality = ~~$cardinalityTween;
    $: sizeTween.set(sizeInBytes || 0);

    let selectingColumns = false;
    let selectedColumns = [];

    const contextButtonId = guidGenerator();

    let clickOutsideListener;
    $: if (!contextMenuOpen && clickOutsideListener) {
        clickOutsideListener();
        clickOutsideListener = undefined;
    }

    // state for title bar hover.
    let titleElementHovered = false;
</script>

<NavEntry
    expanded={show}
    selected={emphasizeTitle}
    bind:hovered={titleElementHovered}
    on:shift-click={async () => {
        await navigator.clipboard.writeText(name);
        notificationStore.send({ message: `copied "${name}" to clipboard` });
    }}
    on:select-body={async (event) => {
        dispatch("select");
    }}
    on:expand={() => {
        show = !show;
        // pass up expand
        dispatch("expand");
    }}
>
    <svelte:fragment slot="tooltip-content">
        <TooltipTitle>
            <svelte:fragment slot="name">
                {name}
            </svelte:fragment>
            <svelte:fragment slot="description" />
        </TooltipTitle>
        <TooltipShortcutContainer>
            <div>open in workspace</div>
            <Shortcut>click</Shortcut>
            <div>
                <StackingWord>copy</StackingWord> to clipboard
            </div>
            <Shortcut>shift + click</Shortcut>
        </TooltipShortcutContainer>
    </svelte:fragment>
    <!-- note: the classes in this span are also used for UI tests. -->
    <span
        class="collapsible-table-summary-title w-full"
        class:is-active={emphasizeTitle}
        class:font-bold={emphasizeTitle}
        class:italic={selectingColumns}
    >
        {#if name.split(".").length > 1}
            {name.split(".").slice(0, -1).join(".")}
            <span class="text-gray-500 italic pl-1">
                .{name.split(".").slice(-1).join(".")}
            </span>
        {:else}
            {name}
        {/if}
        {#if selectingColumns}&nbsp;<span class="font-bold"> *</span>{/if}
    </span>
    <svelte:fragment slot="contextual-information">
        <div class="italic text-gray-600">
            {#if selectingColumns}
                <span>
                    {#if selectedColumns.length}
                        selected {selectedColumns.length} column{#if selectedColumns.length > 1}s{/if}
                    {:else}
                        select columns
                    {/if}
                </span>
            {:else}
                <span
                    class="grid grid-flow-col gap-x-2 text-gray-500 text-clip overflow-hidden whitespace-nowrap "
                >
                    {#if titleElementHovered || emphasizeTitle}
                        <span>
                            <span>
                                {cardinality !== undefined &&
                                !isNaN(cardinality)
                                    ? formatInteger(interimCardinality)
                                    : "no"}
                            </span>
                            row{#if cardinality !== 1}s{/if}
                        </span>
                        <span class="self-center">
                            <ContextButton
                                id={contextButtonId}
                                tooltipText="delete"
                                suppressTooltip={contextMenuOpen}
                                on:click={async (event) => {
                                    contextMenuOpen = !contextMenuOpen;
                                    menuX = event.clientX;
                                    menuY = event.clientY;

                                    if (!clickOutsideListener) {
                                        await tick();
                                        clickOutsideListener = onClickOutside(() => {
                                            contextMenuOpen = false;
                                        }, contextMenu);
                                    }
                                }}>
                                <MoreIcon />
                            </ContextButton>
                        </span>
                    {/if}
                </span>
            {/if}
        </div>
    </svelte:fragment>
</NavEntry>
