<script>
  // # # # # # # # # # # # # #
  //
  //  USERNAME DIALOG
  //
  // # # # # # # # # # # # # #
  // *** IMPORTS
  import { onMount, createEventDispatcher } from "svelte"
  import { fade } from "svelte/transition"
  import { quartOut } from "svelte/easing"
  import sample from "lodash/sample.js"

  // *** STORES
  import { localUserName } from "../stores.js"
  import { urlFor } from "../sanity.js"

  // *** CONSTANTS
  const dispatch = createEventDispatcher()

  // *** VARIABLES
  let username = $localUserName ? $localUserName : ""
  let stepTwo = false

  // *** DOM REFERENCES
  let inputEl = {}

  // *** AVATARS
  export let avatars = []
  let selectedAvatar = sample(avatars)._id

  onMount(async () => {
    if (inputEl) {
      inputEl.focus()
    }
  })
</script>

{#if stepTwo}
  <div
    class="username-dialog"
    transition:fade={{ duration: 400, easing: quartOut }}
  >
    <div class="box avatar-picker">
      <div class="header">Select your avatar</div>
      <div class="inner">
        {#each avatars as avatar, i}
          <div
            class="avatar"
            class:selected={selectedAvatar == avatar._id}
            on:click={() => {
              selectedAvatar = avatar._id
            }}
          >
            <img src={urlFor(avatar.front[0].asset).url()} />
          </div>
        {/each}
      </div>
      <button
        on:click={e => {
          dispatch("username", { username: username, avatar: selectedAvatar })
        }}>Enter</button
      >
    </div>
  </div>
{:else}
  <div
    class="username-dialog"
    transition:fade={{ duration: 400, easing: quartOut }}
  >
    <div class="box">
      <input
        type="text"
        bind:this={inputEl}
        bind:value={username}
        placeholder="Choose your username"
        on:keydown={e => {
          if (e.key == "Enter") stepTwo = true
        }}
      />
      <button
        on:click={e => {
          stepTwo = true
        }}>Enter</button
      >
    </div>
  </div>
{/if}

<style lang="scss">
  @import "../variables.scss";

  .username-dialog {
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    background: black;
    color: white;
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 100000;

    .box {
      font-family: $MONO_STACK;
      padding: 40px;
      font-size: 18px;
      text-align: center;
      user-select: none;
      border-radius: $border_radius;
      background: $COLOR_LIGHT;
      display: flex;

      @include screen-size("small") {
        font-size: 12px;
      }

      input {
        font-family: $MONO_STACK;
        font-size: $FONT_SIZE_MEDIUM;
        float: left;
        width: calc(100% - 60px);
        display: block;
        background: $COLOR_MID_1;
        border: 1px solid $COLOR_DARK;
        color: $COLOR_DARK;
        border-radius: $border_radius;
        padding: $SPACE_S $SPACE_M;
        outline: none;
        height: 30px;
        margin-right: $SPACE_L;

        &.smaller {
          width: calc(100% - 110px);
        }

        &:focus {
          border: 1px solid $COLOR_LIGHT;
        }

        &::placeholder {
          opacity: 0.7;
        }

        input[type="text"] {
          -webkit-appearance: none;
          &::placeholder {
            color: $COLOR_LIGHT;
          }
        }

        select {
          -webkit-appearance: none;
        }
      }

      &.avatar-picker {
        flex-direction: column;
        align-items: center;

        .header {
          font-family: $MONO_STACK;
          color: $COLOR_DARK;
          font-size: $FONT_SIZE_MEDIUM;
        }

        .inner {
          display: flex;
          flex-wrap: wrap;
          margin-top: 20px;
          margin-bottom: 20px;

          .avatar {
            cursor: pointer;
            padding: 5px;
            border: 2px solid transparent;
            border-radius: 5px;
            width: 60px;
            height: 60px;

            img {
              max-width: 100%;
              max-height: 100%;
            }

            @include screen-size("small") {
              padding: 10px;
            }

            &.selected {
              border: 2px solid $COLOR_DARK;
            }
          }
        }
      }
    }
  }

  button {
    font-family: $MONO_STACK;
    font-size: 90%;
    text-transform: uppercase;
    float: right;
    display: block;
    width: 100px;
    background: transparent;
    border: 1px solid $COLOR_DARK;
    color: $COLOR_DARK;
    border-radius: $border_radius;
    outline: none;
    cursor: pointer;
    height: 30px;
    line-height: 20px;

    &:hover {
      border: 1px solid $COLOR_LIGHT;
      background: $COLOR_MID_1;
    }
  }
</style>
