<script setup></script>

<template>
    <div class="content">
        <section class="about">
            <h1 class="about_title">About</h1>
            <div class="about_content">
                <p>"Captioned" is a modern, geometric, slab serif font inspired by Hideo Sato's <em>Cinema Font</em>. It
                    was
                    created as a personal project, born out of curiosity about typeface design.</p>
                <p>The character ranges currently supported are <a href="https://www.unicode.org/charts/PDF/U0000.pdf"
                        target="_blank">Basic Latin</a> and <a href="https://www.unicode.org/charts/PDF/U0080.pdf"
                        target="_blank">Latin-1 Supplement</a>, making "Captioned" a simple yet versatile font.</p>
                <p>You can check the <a href="https://github.com/samuelquiros-design/captioned" target="_blank">GitHub
                        repository</a> to report issues or contribute.</p>
            </div>
        </section>
        <section class="specs">
            <h1 class="specs_title">Specifications</h1>
            <div class="specs_content">
                <div class="specs_item">
                    <h2 class="specs_item_title">Name</h2><span class="specs_item_info">Captioned</span>
                </div>
                <div class="specs_item">
                    <h2 class="specs_item_title">Designer</h2><span class="specs_item_info"><a
                            href="https://github.com/samuelquiros-design" target="_blank">Samuel Quirós</a></span>
                </div>
                <div class="specs_item">
                    <h2 class="specs_item_title">Category</h2><span class="specs_item_info">Slab serif, Geometric</span>
                </div>
                <div class="specs_item">
                    <h2 class="specs_item_title">Styles</h2><span class="specs_item_info">Regular</span>
                </div>
                <div class="specs_item">
                    <h2 class="specs_item_title">Version</h2><span class="specs_item_info">1.0.0</span>
                </div>
                <div class="specs_item">
                    <h2 class="specs_item_title">License</h2><span class="specs_item_info">Open Source (GNU AGPL)</span>
                </div>
            </div>
        </section>
    </div>
</template>

<style scoped lang="scss">
.content {
    display: flex;
    align-items: start;
    justify-content: space-between;
    width: 100%;
    padding: 2rem 4rem;
    gap: 4rem;
    overflow-y: auto;
    font-size: clamp(1rem, 2.5vw, 1.25rem);

    .about {
        display: flex;
        flex-direction: column;
        gap: 1.5rem;
        width: 60%;

        .about_content {
            display: flex;
            flex-direction: column;
            gap: .75rem;
        }
    }

    .specs {
        display: flex;
        flex-direction: column;
        gap: 1.5rem;
        flex: 1;

        .specs_content {
            display: flex;
            flex-direction: column;

            .specs_item {
                display: flex;
                align-items: center;
                gap: 1rem;
                padding: 1rem;
                border-bottom: 2px solid $color_dark;

                &:first-child {
                    border-top: 2px solid $color_dark;
                }

                .specs_item_title {
                    display: flex;
                    width: 40%;
                }

                .specs_item_info {
                    display: flex;
                    flex: 1;
                }
            }
        }
    }
}

@media (max-width: 1024px) {
    .content {

        .about {
            width: 50%;
        }
    }
}

@media (max-width: 768px) {
    .content {
        flex-direction: column;
        width: 100%;
        gap: 2rem;

        .about {
            width: 100%;
            gap: .75rem;

            .about_content {
                gap: .5rem;
            }
        }

        .specs {
            width: 100%;
            gap: .75rem;

            .specs_content {
                gap: .5rem;

                .specs_item {
                    gap: .75rem;
                    padding: .75rem;

                    .specs_item_title {
                        width: 50%;
                    }

                    .specs_item_info {
                        flex: 1;
                    }
                }
            }
        }
    }
}

@supports (-webkit-touch-callout: none) {
    .content {
        padding-bottom: 8rem;
    }
}
</style>
