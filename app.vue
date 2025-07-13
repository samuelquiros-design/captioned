<script setup>
import { ref } from 'vue'

const is_menu_open = ref(false)

function toggle_menu() {
  is_menu_open.value = !is_menu_open.value
}

function reset_scroll() {
  is_menu_open.value = false
  window.scrollTo({ top: 0, behavior: 'smooth' })

  const scrollables = document.querySelectorAll('*')
  scrollables.forEach(el => {
    const has_vertical_scroll = el.scrollHeight > el.clientHeight
    if (has_vertical_scroll) {
      el.scrollTo?.({ top: 0, behavior: 'smooth' })
    }
  })
}
</script>

<template>
  <div class="content_wrapper">
    <div class="overlay" :class="{ 'overlay_visible': is_menu_open }" @click="is_menu_open = false"></div>

    <button class="menu_toggle" @click="toggle_menu">
      <span class="material-symbols-rounded">
        {{ is_menu_open ? 'close' : 'menu' }}
      </span>
    </button>

    <button class="scroll_reset" @click="reset_scroll" aria-label="Reset scroll">
      <span class="material-symbols-rounded">arrow_upward</span>
    </button>

    <header :class="['header', { open: is_menu_open }]">
      <div class="header_single">
        <NuxtLink to="/" class="header_title" @click="is_menu_open = false">Captioned</NuxtLink>
        <ul class="header_nav" @click="is_menu_open = false">
          <li class="nav_details">
            <NuxtLink to="/">Details</NuxtLink>
          </li>
          <li class="nav_tester">
            <NuxtLink to="/tester">Type Tester</NuxtLink>
          </li>
          <li class="nav_glyphs">
            <NuxtLink to="/glyphs">Glyphs</NuxtLink>
          </li>
          <li class="nav_license">
            <NuxtLink to="/license">License</NuxtLink>
          </li>
        </ul>
        <a href="https://github.com/samuelquiros-design/captioned/releases/latest/download/Captioned.otf"
          class="header_download">
          <span class="material-symbols-rounded download_icon">download</span>
          <span class="download_text">Download</span>
        </a>
      </div>
      <div class="header_double">
        <ul class="header_double_nav">
          <li class="nav_details">
            <NuxtLink to="/">Details</NuxtLink>
          </li>
          <li class="nav_tester">
            <NuxtLink to="/tester">Type Tester</NuxtLink>
          </li>
          <li class="nav_glyphs">
            <NuxtLink to="/glyphs">Glyphs</NuxtLink>
          </li>
          <li class="nav_license">
            <NuxtLink to="/license">License</NuxtLink>
          </li>
        </ul>
      </div>
    </header>

    <main class="main">
      <NuxtPage />
    </main>
  </div>
</template>

<style scoped lang="scss">
.content_wrapper {
  color: $color_dark;
  background-color: $color_light;

  .overlay {
    position: fixed;
    inset: 0;
    background-color: $color_dark;
    opacity: 0;
    pointer-events: none;
    transition: opacity 0.3s ease-in-out;
    z-index: 2;
    cursor: default;

    &.overlay_visible {
      opacity: 0.25;
      pointer-events: auto;
    }
  }

  .menu_toggle {
    display: none;
    align-items: center;
    justify-content: center;
    width: 3rem;
    height: 3rem;
    position: fixed;
    bottom: .5rem;
    right: .5rem;
    z-index: 4;
    background-color: $color_light;
    border: 2px solid $color_dark;
    border-radius: 1.5rem;
    cursor: pointer;

    .material-symbols-rounded {
      font-size: 2rem;
    }

    &:hover {
      border: 4px solid $color_dark;

      .material-symbols-rounded {
        font-weight: 600;
      }
    }
  }

  .scroll_reset {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 3rem;
    height: 3rem;
    position: fixed;
    bottom: .5rem;
    left: .5rem;
    z-index: 4;
    background-color: $color_light;
    border: 2px solid $color_dark;
    border-radius: 1.5rem;
    cursor: pointer;

    .material-symbols-rounded {
      font-size: 2rem;
    }

    &:hover {
      border: 4px solid $color_dark;

      .material-symbols-rounded {
        font-weight: 600;
      }
    }
  }

  .header {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    position: fixed;
    top: 0;
    z-index: 3;
    width: 100vw;
    height: 6rem;
    background-color: $color_light;

    .header_single {
      display: flex;
      align-items: center;
      justify-content: space-between;
      width: 100%;
      height: 6rem;

      .header_title {
        display: flex;
        align-items: center;
        justify-content: center;
        font-family: 'Captioned';
        font-size: clamp(2.5rem, 2.5vw, 3rem);
        padding: 0 2rem;
        width: 20%;
        height: 100%;
        border-top: 2px solid transparent;
        border-bottom: 2px solid $color_dark;

        &:hover {
          border-top: 4px solid transparent;
          border-bottom: 4px solid $color_dark;
        }
      }

      .header_nav {
        display: flex;
        align-items: center;
        justify-content: space-around;
        height: 100%;
        flex: 1;

        li {
          display: flex;
          align-items: center;
          justify-content: center;
          height: 100%;
          flex: 1;

          a {
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: clamp(1rem, 2.5vw, 1.25rem);
            padding: 0 1rem;
            width: 100%;
            height: 100%;
            border-top: 2px solid transparent;
            border-bottom: 2px solid $color_dark;

            &:hover {
              border-top: 4px solid transparent;
              border-bottom: 4px solid $color_dark;
              font-weight: 600;
            }

            &.router-link-active {
              border-top: 4px solid transparent;
              border-bottom: 4px solid $color_dark;
              font-weight: 600;
            }
          }
        }
      }

      .header_download {
        display: flex;
        align-items: center;
        justify-content: center;
        padding: 0 2rem;
        gap: 1rem;
        width: 20%;
        height: 100%;
        border-top: 2px solid transparent;
        border-bottom: 2px solid $color_dark;

        &:hover {
          border-top: 4px solid transparent;
          border-bottom: 4px solid $color_dark;
        }

        span {
          font-size: clamp(1.5rem, 2.5vw, 2rem);
        }
      }
    }

    .header_double {
      display: none;
      align-items: center;
      justify-content: space-between;
      width: 100%;
      height: 3rem;

      .header_double_nav {
        display: flex;
        align-items: center;
        justify-content: space-around;
        height: 100%;
        flex: 1;

        li {
          display: flex;
          align-items: center;
          justify-content: center;
          height: 100%;
          flex: 1;

          a {
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: clamp(1rem, 2.5vw, 1.25rem);
            padding: 0 2rem;
            width: 100%;
            height: 100%;
            border-top: 2px solid transparent;
            border-bottom: 2px solid $color_dark;

            &:hover {
              border-top: 4px solid transparent;
              border-bottom: 4px solid $color_dark;
              font-weight: 600;
            }

            &.router-link-active {
              border-top: 4px solid transparent;
              border-bottom: 4px solid $color_dark;
              font-weight: 600;
            }
          }
        }
      }
    }
  }

  .main {
    display: flex;
    width: 100vw;
    height: calc(100vh - 6rem);
    margin-top: 6rem;
  }

  @media (max-width: 1024px) {
    .header {
      height: 9rem;

      .header_single {
        justify-content: space-around;

        .header_title {
          width: 100%;
        }

        .header_nav {
          display: none;
        }

        .header_download {
          width: 100%;
        }
      }

      .header_double {
        display: flex;
      }
    }

    .main {
      margin-top: 9rem;
    }
  }

  @media (max-width: 768px) {
    .menu_toggle {
      display: flex;
    }

    .header {
      width: 100vw;
      height: fit-content;
      background-color: $color_light;
      position: fixed;
      top: auto;
      bottom: 0;
      border-top: 2px solid $color_dark;
      transform: translateY(100%);
      transition: transform 0.3s ease-in-out;

      &.open {
        transform: translateY(0%);
      }

      .header_single {
        flex-direction: column;
        justify-content: start;
        width: 100%;
        height: 100%;
        border: none;

        .header_title {
          width: 100%;
          height: 8rem;
          padding: 0;
          border-top: 2px solid transparent;
          border-bottom: 2px solid transparent;
        }

        .header_nav {
          display: flex;
          flex-direction: column;
          width: 100%;
          flex: 0;

          li {
            width: 100%;

            a {
              padding: 0;
              height: 4rem;
              border: none;

              &:hover {
                border: none;
                text-decoration: underline;
                text-decoration-thickness: 4px;
                text-underline-offset: 1rem;
              }

              &.router-link-active {
                border: none;
                text-decoration: underline;
                text-decoration-thickness: 4px;
                text-underline-offset: 1rem;
              }
            }
          }
        }

        .header_download {
          flex-direction: column;
          gap: 0;
          width: 100%;
          height: 8rem;
          padding: 0;
          border: none;

          .download_icon {
            font-size: 2rem;
            font-weight: 300;
          }
        }
      }

      .header_double {
        display: none;
      }
    }

    .main {
      height: 100vh;
      margin: 0;
    }
  }
}
</style>