<script>
  import { blur, fade, fly } from "svelte/transition";


</script>

<div class="modal-container" in:blur out:fade>
    <div class="modal-content" transition:fly={{y:200}}>
        <!--
            <slot name="header"/>
            <slot name="footer"/>
        -->
        <slot><!--Default modal content here--></slot>
    </div>
</div>