<script setup>
import { ref, onMounted } from 'vue'

const selected_glyph = ref(null)

const unicode_ranges = [
    { name: 'Basic Latin', start: 0x20, end: 0x7E },
    { name: 'Latin-1 Supplement', start: 0xA0, end: 0xFF }
]

const glyphs_per_range = ref({})

function supports_glyph(char, font) {
    const canvas = document.createElement('canvas')
    const ctx = canvas.getContext('2d')
    canvas.width = 50
    canvas.height = 50

    ctx.clearRect(0, 0, 50, 50)
    ctx.textBaseline = 'top'

    ctx.font = `40px ${font}, monospace`
    ctx.fillText(char, 0, 0)
    const data1 = ctx.getImageData(0, 0, 50, 50).data

    ctx.clearRect(0, 0, 50, 50)
    ctx.font = `40px monospace`
    ctx.fillText(char, 0, 0)
    const data2 = ctx.getImageData(0, 0, 50, 50).data

    for (let i = 0; i < data1.length; i++) {
        if (data1[i] !== data2[i]) return true
    }
    return false
}

onMounted(() => {
    const font_name = "'Captioned', sans-serif"
    const new_glyphs_per_range = {}

    unicode_ranges.forEach(range => {
        const candidate_chars = []
        for (let i = range.start; i <= range.end; i++) {
            candidate_chars.push(String.fromCharCode(i))
        }
        new_glyphs_per_range[range.name] = candidate_chars.filter(char => supports_glyph(char, font_name))
    })

    glyphs_per_range.value = new_glyphs_per_range

    for (const range_name of Object.keys(glyphs_per_range.value)) {
        if (glyphs_per_range.value[range_name].length > 0) {
            selected_glyph.value = glyphs_per_range.value[range_name][0]
            break
        }
    }
})
</script>

<template>
    <div class="content">
        <div class="glyph_preview">
            <span v-if="selected_glyph" class="preview_char">{{ selected_glyph }}</span>
        </div>

        <div class="glyph_ranges">
            <section v-for="(glyphs, range_name) in glyphs_per_range" :key="range_name" class="glyph_range_section">
                <h2 class="range_header">{{ range_name }}</h2>
                <div class="glyph_map">
                    <div v-for="(glyph, index) in glyphs" :key="glyph + index" class="glyph_cell"
                        :class="{ selected: selected_glyph === glyph }" @click="selected_glyph = glyph">
                        {{ glyph }}
                    </div>
                </div>
            </section>
        </div>
    </div>
</template>

<style scoped lang="scss">
.content {
    display: flex;
    align-items: start;
    width: 100%;
    gap: 4rem;
    padding: 0 4rem;

    .glyph_preview {
        display: flex;
        align-items: center;
        justify-content: center;
        width: 40%;
        height: 100%;
        font-size: 20rem;
        color: $color_dark;
        text-align: center;
        background-color: $color_light;
        font-family: 'Captioned', sans-serif;

        .preview_char {
            display: flex;
            align-items: center;
            justify-content: center;
            width: 16rem;
            height: 16rem;
            line-height: 16rem;
            text-align: center;
        }
    }

    .glyph_ranges {
        display: flex;
        flex-direction: column;
        gap: 6rem;
        padding: 2rem 0;
        width: 60%;
        height: 100%;
        overflow: auto;

        .glyph_range_section {

            .range_header {
                margin-bottom: 2rem;
                font-size: 3rem;
                font-weight: 400;
                color: $color_dark;
            }

            .glyph_map {
                display: grid;
                grid-template-columns: repeat(auto-fill, 4rem);
                justify-content: center;
                gap: 1rem;
                overflow-x: hidden;
                font-family: 'Captioned', sans-serif;
                color: $color_medium;

                .glyph_cell {
                    box-sizing: border-box;
                    display: flex;
                    align-items: center;
                    justify-content: center;
                    width: 4rem;
                    height: 4rem;
                    font-size: 3rem;
                    text-align: center;
                    border-radius: 0.5rem;
                    cursor: pointer;

                    &:hover {
                        border: 2px solid $color_dark;
                        color: $color_dark;
                    }

                    &.selected {
                        background-color: $color_dark;
                        color: $color_light;
                    }
                }
            }
        }
    }
}

@media (max-width: 768px) {
    .content {
        flex-direction: column;
        align-items: center;
        width: 100%;
        gap: 2rem;

        .glyph_preview {
            position: fixed;
            width: 100vw;
            height: 25vh;
            font-size: 8rem;
            padding: 1rem 0;
            border-top: 2px solid transparent;
            border-bottom: 2px solid $color_dark;

            .preview_char {
                width: 8rem;
                height: 8rem;
                line-height: 8rem;
                text-align: center;
            }
        }

        .glyph_ranges {
            width: 100%;
            gap: 4rem;
            margin-top: 25vh;

            .glyph_range_section {

                .range_header {
                    margin-bottom: 1rem;
                    font-size: 2rem
                }

                .glyph_map {
                    gap: 0.5rem;

                    .glyph_cell {
                        width: 3rem;
                        height: 3rem;
                        font-size: 2rem;
                    }
                }
            }
        }
    }
}
</style>