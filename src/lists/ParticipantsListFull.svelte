<script>
  // # # # # # # # # # # # # #
  //
  //  Participants List Full
  //
  // # # # # # # # # # # # # #

  // *** IMPORTS
  import get from "lodash/get"
  import { renderBlockText } from "../sanity.js"

  // *** PROPS
  export let participants = {}

  // *** STORES
  import { globalSettings } from "../stores.js"
</script>

<div class="case-study-container">
  <!-- HEADER -->
  <div class="case-study-item header">
    <div class="inner">
      <div class="row">
        <div>GameChangers</div>
      </div>
    </div>
  </div>

  <!-- PEOPLE -->
  {#each participants as user, index (user._id)}
    <a
      class="case-study-item"
      href={"/people/" + get(user, "slug.current", "")}
    >
      <div class="inner">
        <div class="mid-section">
          <div class="title">{user.name}</div>
        </div>
      </div>
    </a>
  {/each}
</div>

<style lang="scss">
  @import "../variables.scss";

  .case-study-container {
    height: 100%;
    color: $COLOR_DARK;
    font-family: $MONO_STACK;
    font-size: $FONT_SIZE_BASE;
    background: $COLOR_LIGHT;

    .case-study-item {
      padding: 0px $SPACE_S;
      padding-top: $SPACE_S;
      padding-bottom: $SPACE_S;
      width: 100%;
      // min-height: $ITEM_HEIGHT;
      background: $COLOR_LIGHT;
      color: $COLOR_DARK;
      display: inline-block;
      text-decoration: none;
      user-select: none;

      .inner {
        width: 100%;

        .color-icon {
          display: none;
          height: 10px;
          width: 10px;
          margin-right: $SPACE_M;
          float: left;
          margin-top: 4px;
          background: $COLOR_EXHIBITION;

          &.communication {
            background: $COLOR_COMMUNICATION;
          }
          &.consensus-building {
            background: $COLOR_CONSENSUS_BUILDING;
          }
          &.sensing {
            background: $COLOR_SENSING;
          }
          &.archiving {
            background: $COLOR_ARCHIVING;
          }
        }

        .mid-section {
          width: 60%;
          float: left;

          .title {
            font-family: $SANS_STACK;
            font-weight: 500;
          }

          .participants {
            font-family: $MONO_STACK;
            pointer-events: none;
            color: $COLOR_MID_2;
            font-size: $FONT_SIZE_SMALL;
          }
        }

        .date {
          white-space: nowrap;
          color: $COLOR_MID_2;
          float: right;
        }
      }

      transition: background 0.5s $transition;

      &:hover {
        background: $COLOR_MID_1;
      }

      &.header {
        height: 45px;
        border-bottom: 1px solid $COLOR_MID_1;
        background-color: white;
        // word-spacing: -0.3em;
        &:hover {
          background: white !important;
        }
        &.related {
          background-color: unset;
          &:hover {
            background: unset !important;
          }
        }
        .archive-link {
          color: $COLOR_MID_2;
          text-decoration: underline;
        }

        &:hover {
          background: unset;
        }
      }

      &.related {
        padding-left: 0;
        padding-right: 0;

        &.header {
          height: 30px;
          padding-top: 0;
        }
      }
    }

    .description {
      padding: $SPACE_S;
    }

    .toolbar {
      width: 100%;
      display: flex;
      justify-content: space-between;
      align-items: center;
      height: 45px;
      padding: $SPACE_S;
      font-size: $FONT_SIZE_SMALL;
      border-bottom: 1px dotted $COLOR_MID_1;
      margin-bottom: $SPACE_S;

      .sort {
        height: 100%;
        display: flex;
        align-items: center;

        select {
          margin-left: $SPACE_XS;
          font-size: $FONT_SIZE_SMALL;
          color: $COLOR_DARK;
          font-family: $MONO_STACK;
          border: none;
          background: $COLOR_LIGHT;
        }
      }

      .filter {
        height: 100%;
        display: flex;
        align-items: center;

        svg {
          margin-right: $SPACE_XS;
          path {
            color: $COLOR_MID_1;
          }
        }
        input {
          width: 8ch;
          border: none;
          outline: none;
          font-size: $FONT_SIZE_SMALL;
          color: $COLOR_DARK;
          font-family: $MONO_STACK;
          background: $COLOR_LIGHT;

          input[type="text"] {
            -webkit-appearance: none;
          }

          select {
            -webkit-appearance: none;
          }

          &:focus {
            border-bottom: 1px solid $COLOR_DARK;
            width: 16ch;
          }
        }
      }
    }
  }
</style>
