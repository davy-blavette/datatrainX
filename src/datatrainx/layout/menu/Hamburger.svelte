<script>
    export let open = false

</script>
<style>
    button{
        background: none;
        border: none;
    }
    svg {
        min-height: 24px;
        transition: transform 0.3s ease-in-out;
        color:white;
    }

    svg line {
        stroke: currentColor;
        stroke-width: 3;
        transition: transform 0.3s ease-in-out
    }

    button {
        z-index: 20;
        cursor: pointer;
    }

    .open svg {
        transform: scale(0.7)
    }

    .open #top {
        transform: translate(6px, 0px) rotate(45deg)
    }

    .open #middle {
        opacity: 0;
    }

    .open #bottom {
        transform: translate(-12px, 9px) rotate(-45deg)
    }
</style>
<button class="" class:open on:click={() => open = !open}>
    <svg width=32 height=24>
        <line id="top" x1=0 y1=2  x2=32 y2=2/>
            <line id="middle" x1=0 y1=12 x2=24 y2=12/>
                <line id="bottom" x1=0 y1=22 x2=32 y2=22/>
    </svg>
</button>

