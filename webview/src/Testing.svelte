<script>
  export let data;
  export let edit;
  export let craete;

  const timeOptions = [
    `0.1s`,
    `0.25s`,
    `0.5s`,
    `1s`,
    `2s`,
    `3s`,
    `4s`,
    `5s`,
    `10s`,
    `15s`,
    `30s`,
    `1m`,
    `3m`,
    `5m`,
  ];

  const codeOptions = [
    `OK`,
    `Cancelled`,
    `Unknown`,
    `InvalidArgument`,
    `DeadlineExceeded`,
    `NotFound`,
    `AlreadyExists`,
    `PermissionDenied`,
    `ResourceExhausted`,
    `FailedPrecondition`,
    `Aborted`,
    `OutOfRange`,
    `Unimplemented`,
    `Internal`,
    `Unavailable`,
    `DataLoss`,
    `Unauthenticated`,
  ];

  $: innerHeight = 0;
</script>

<svelte:window bind:innerHeight />

<table>
  <tr>
    <vscode-data-grid aria-label="Basic">
      <vscode-data-grid-row>
        <vscode-data-grid-cell grid-column="1" class="dropdown">
          <b>Expected time</b>
        </vscode-data-grid-cell>
        <vscode-data-grid-cell grid-column="2">
          <vscode-dropdown position="below">
            {#each timeOptions as time}
              <vscode-option
                on:click="{() => {
                  data.expectedTime = time;
                }}"
              >
                <div>{time}</div>
              </vscode-option>
            {/each}
          </vscode-dropdown>
        </vscode-data-grid-cell>
      </vscode-data-grid-row>
      <vscode-data-grid-row>
        <vscode-data-grid-cell grid-column="1" class="dropdown">
          <b>Expected code</b>
        </vscode-data-grid-cell>
        <vscode-data-grid-cell grid-column="2">
          <vscode-dropdown position="below">
            {#each codeOptions as code}
              <vscode-option
                on:click="{() => {
                  data.expectedCode = code;
                }}"
              >
                <div>{code}</div>
              </vscode-option>
            {/each}
          </vscode-dropdown>
        </vscode-data-grid-cell>
      </vscode-data-grid-row>
    </vscode-data-grid>
  </tr>
  <tr>
    <center>
      <b>Expected response JSON</b>
    </center>
  </tr>
  <tr>
    <textarea
      name=""
      id=""
      cols="30"
      rows="10"
      style="--height: {innerHeight - 320}px"
      bind:value="{data.expectedResponse}"
      on:input="{edit}"></textarea>
  </tr>
  <tr>
    <div class="button-padding">
      <center>
        <button on:click="{craete}">Create test</button>
      </center>
    </div>
  </tr>
</table>

<style>
  vscode-dropdown {
    width: 100%;
  }
  vscode-option {
    width: 100%;
  }
  .button-padding {
    padding-top: 10px;
    padding-left: 30px;
    padding-right: 30px;
  }
  button {
    border: none;
    padding: var(--input-padding-vertical) var(--input-padding-horizontal);
    width: 100%;
    text-align: center;
    outline: 1px solid transparent;
    outline-offset: 2px !important;
    color: var(--vscode-button-foreground);
    background: var(--vscode-button-background);
    padding-top: 6px;
    padding-bottom: 6px;
  }
  button:hover {
    cursor: pointer;
    background: var(--vscode-button-hoverBackground);
  }
  button:focus {
    outline-color: var(--vscode-focusBorder);
  }
  table {
    width: 100%;
  }
  tr {
    width: 100%;
  }
  .dropdown {
    padding-top: 10px;
  }
  textarea {
    height: var(--height);
    resize: none;
    display: block;
    width: 98%;
    padding: 6px;
    color: var(--vscode-input-foreground);
    outline-color: var(--vscode-input-border);
    background-color: var(--vscode-input-background);
    font-family: var(--vscode-editor-font-family);
    font-size: var(--vscode-editor-font-size);
  }
  center {
    padding-top: 10px;
    padding-bottom: 5px;
  }
</style>
