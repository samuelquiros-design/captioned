<script setup>
import { ref, watch, onMounted } from 'vue'

const user_input = ref('')
const is_focused = ref(false)
const input_ref = ref(null)
const font_size = ref(48)
const slider_ref = ref(null)
const slider_min_value = 8
const slider_max_value = 256

const update_slider_style = () => {
    const val = font_size.value
    const percent = ((val - slider_min_value) / (slider_max_value - slider_min_value)) * 100
    if (slider_ref.value) {
        slider_ref.value.style.setProperty('--val', `${percent}%`)
    }
}

watch(font_size, update_slider_style)

onMounted(() => {
    update_slider_style()
})

function focus_input() {
    input_ref.value?.focus()
}
</script>

<template>
    <div class="content">
        <div class="tester_input">
            <div class="tester_form" :class="{ typing: user_input, focused: is_focused }" @click="focus_input">
                <span class="material-symbols-rounded">stylus</span>
                <input id="user_input" ref="input_ref" v-model="user_input" placeholder="Write here"
                    @focus="is_focused = true" @blur="is_focused = false" />
            </div>
            <div class="tester_slider">
                <span class="size_current">{{ font_size + 'px' }}</span>
                <input ref="slider_ref" class="size_slider" type="range" min="8" max="256" step="4" v-model="font_size"
                    @click.stop />
            </div>
        </div>
        <div class="tester_preview">
            <p class="tester_output" :style="{ fontSize: font_size + 'px' }">
                {{ user_input || 'Captioned Regular' }}
            </p>
        </div>
    </div>
</template>

<style scoped lang="scss">
.content {
    display: flex;
    flex-direction: column;
    align-items: start;
    width: 100%;
    padding: 2rem 4rem;
    gap: 4rem;
    overflow-y: auto;

    .tester_input {
        display: flex;
        align-items: center;
        justify-content: space-between;
        width: 100%;
        gap: 2rem;

        .tester_form {
            display: flex;
            align-items: center;
            justify-content: start;
            width: 50%;
            gap: .5rem;
            padding: .25rem .5rem;
            border-bottom: 2px solid $color_medium;
            cursor: text;

            span {
                font-size: 1.5rem;
                color: $color_medium;
            }

            input {
                font-size: 1.5rem;
                color: $color_medium;
                width: 100%;
            }

            &:hover {
                border-bottom: 2px solid $color_dark;

                span,
                input {
                    color: $color_dark;
                }
            }

            &.typing,
            &.focused {
                border-bottom: 2px solid $color_dark;

                span,
                input {
                    color: $color_dark;
                }
            }
        }

        .tester_slider {
            display: flex;
            align-items: center;
            justify-content: end;
            gap: 1rem;

            .size_current {
                display: flex;
                justify-content: end;
            }

            .size_slider {
                cursor: pointer;
                width: 128px;
                height: 2px;
                border-radius: 2px;
                background: transparent;

                &::-webkit-slider-runnable-track {
                    height: 4px;
                    border-radius: 2px;
                    background: linear-gradient(to right,
                            $color_dark 0%,
                            $color_dark var(--val),
                            $color_medium var(--val),
                            $color_medium 100%);
                }

                &::-webkit-slider-thumb {
                    -webkit-appearance: none;
                    height: 16px;
                    width: 16px;
                    border-radius: 50%;
                    background: $color_dark;
                    margin-top: -6px;
                    position: relative;
                    z-index: 1;
                }

                &::-moz-range-track {
                    height: 2px;
                    border-radius: 2px;
                    background: $color_medium;
                }

                &::-moz-range-progress {
                    height: 4px;
                    border-radius: 2px;
                    background: $color_dark;
                }

                &::-moz-range-thumb {
                    height: 16px;
                    width: 16px;
                    border-radius: 50%;
                    background: $color_dark;
                    border: none;
                }
            }
        }
    }

    .tester_preview {
        display: flex;
        width: 100%;
        padding: 2rem 3rem;
        border: 2px solid $color_dark;

        .tester_output {
            font-family: 'Captioned';
            word-break: break-word;
        }
    }
}

@media (max-width: 768px) {
    .content {
        gap: 2rem;

        .tester_input {
            flex-direction: column;
            align-items: end;

            .tester_form {
                width: 100%;
            }
        }

        .tester_preview {
            padding: 1rem 1.5rem;
        }
    }
}

@supports (-webkit-touch-callout: none) {
    .content {
        padding-bottom: 8rem;
    }
}
</style>