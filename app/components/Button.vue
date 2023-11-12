<template>
    <component
        :is="props.href ? NuxtLink : 'button'"
        :href="props.href"
        :class="[
            props.color,
            `rounded-${props.rounded}`,
            `size-${props.size}`,
            {'activated': props.activated}
        ]"
    >
        <slot />
    </component>
</template>

<script setup lang="ts">
    import { NuxtLink } from "#components";

    const props = withDefaults(defineProps<{
        color?: "transparent" | "primary" | "secondary" | "white"
        href?: string
        rounded?: "full" | "none" | "normal"
        size?: "sm" | "md" | "lg"
        activated?: boolean
    }>(), {
        href: undefined,
        color: "primary",
        rounded: "normal",
        size: "lg"
    });
</script>

<style scoped lang="scss">
    button, a {
        display: inline-flex;
        justify-content: center;
        text-align: center;
        border: none;
        outline: none;
        border-width: 0.0625rem;
        letter-spacing: 0.0625rem;
        border-style: solid;
        border-color: transparent;
        font-weight: 500;
        transition: all .3s ease-in-out;

        &.rounded-normal {
            border-radius: .5rem;
        }

        &.rounded-full {
            border-radius: 9999px;
        }

        &.rounded-none {
            border-radius: none;
        }

        &.size-sm {
            padding: $spacing-2;
            font-size: 0.875rem;
        }

        &.size-md {
            padding: $spacing-2 $spacing-4;
            font-size: 0.875rem;
        }

        &.size-lg {
            padding: $spacing-4 $spacing-6;
            text-transform: uppercase;
            font-size: 1rem;
        }

        &:hover {
            box-shadow: 0 10px 15px -3px rgb(0 0 0 / 0.1), 0 4px 6px -4px rgb(0 0 0 / 0.1);
        }

        &:disabled {
            opacity: .3;
            cursor: not-allowed;
        }

        &.activated {
            cursor: not-allowed;
        }
    }

    .transparent {
        background-color: transparent;
        color: currentColor;

        &:hover,
        &.activated {
            color: $color-primary;
            border-color: $color-primary;
        }
    }

    .primary {
        background-color: $color-primary;
        color: $color-font-invert;

        &:hover,
        &.activated {
            background-color: $color-font-invert;
            color: $color-primary;
            border-color: $color-primary;
        }
    }

    .secondary {
        background-color: $color-secondary;
        color: $color-font-invert;

        &:hover,
        &.activated {
            background-color: $color-font-invert;
            color: $color-secondary;
            border-color: $color-secondary;
        }
    }

    .white {
        background-color: $color-font-invert;
        color: $color-secondary;

        &:hover,
        &.activated {
            background-color: $color-secondary;
            color: $color-font-invert;
            border-color: $color-font-invert;
        }
    }
</style>