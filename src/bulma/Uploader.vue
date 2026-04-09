<template>
    <form class="m-0"
        @submit.prevent>
        <core-uploader v-bind="$attrs"
            ref="uploader">
            <template #default="{
                controlEvents, files, inputBindings, inputEvents, label, manual,
            }">
                <input class="is-hidden"
                    v-bind="inputBindings"
                    v-on="inputEvents">
                <slot name="control"
                    :control-events="controlEvents">
                    <a :class="['button', 'uploader-button', {'is-small': isSmall},
                        {'is-large': isLarge}, {'is-rounded': isRounded}]"
                        v-on="controlEvents">
                        <span class="file-label"
                            v-if="label">
                            {{ label }}
                        </span>
                        <span class="icon"
                            v-if="!manual || files">
                            <fa :icon="faUpload"/>
                        </span>
                    </a>
                </slot>
            </template>
        </core-uploader>
    </form>
</template>

<script>
import { FontAwesomeIcon as Fa } from '@fortawesome/vue-fontawesome';
import { faUpload } from '@fortawesome/free-solid-svg-icons';
import CoreUploader from '../renderless/CoreUploader.vue';

export default {
    name: 'Uploader',

    components: { CoreUploader, Fa },

    data: () => ({
        faUpload,
    }),

    props: {
        isLarge: {
            type: Boolean,
            default: false,
        },
        isRounded: {
            type: Boolean,
            default: false,
        },
        isSmall: {
            type: Boolean,
            default: false,
        },
    },

    methods: {
        browseFiles() {
            this.$refs.uploader.browseFiles();
        },
    },
};
</script>

<style lang="scss">
.uploader-button {
    background-color: var(--bulma-scheme-main);
    border: 1px solid var(--bulma-input-border-color);
    box-shadow: none;
    color: var(--bulma-text-strong);

    &:hover,
    &:focus {
        background-color: var(--bulma-scheme-main-ter);
        border-color: var(--bulma-input-hover-border-color);
        color: var(--bulma-text-strong);
    }
}
</style>
