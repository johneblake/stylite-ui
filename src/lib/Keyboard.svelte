<script lang="ts" context="module">
  export enum KeyboardTypes {
    None,
    Alpha,
    Numeric,
  };
</script>

<script lang="ts">
  import Keyboard from 'simple-keyboard';
  import { onMount, tick, createEventDispatcher } from 'svelte';
  import 'simple-keyboard/build/css/index.css';

  const dispatch = createEventDispatcher();

  export let float = false;

  export let label: string;

  export let hidden = true;

  export let keyboardType: KeyboardTypes = KeyboardTypes.None;

  export let start = '';

  let input = '';

  let init = false;

  let alphaKeyboard: Keyboard;

  let numKeyboard: Keyboard;

  let activeKeyboard: Keyboard;

  let alphaRef: HTMLDivElement;

  let inputRef: HTMLInputElement;

  let numRef: HTMLDivElement;

  let hiddenAlpha = true;

  let hiddenNum = true;

  $: {
    hiddenAlpha = keyboardType !== KeyboardTypes.Alpha;
    hiddenNum = keyboardType !== KeyboardTypes.Numeric;
    activeKeyboard = keyboardType === KeyboardTypes.Numeric ? numKeyboard : alphaKeyboard;
  }

  $: { 
    input = start === ' ' ? '' : start;
    init = true;
  }

  $: {
    activeKeyboard?.setInput(input);
    if (init || activeKeyboard?.caretPosition === null) {
      inputRef?.setSelectionRange(0, input.length);
      activeKeyboard?.setCaretPosition(0, input.length);
      tick()
        .then(() => {
          inputRef?.focus();
        });
      init = false;
    }
  }

  onMount(async () => {
    alphaKeyboard = new Keyboard('.alphaKeyboard', {
      onChange,
      onKeyPress,
      preventMouseDownDefault: true,
      layout: {
        default: [
          "` 1 2 3 4 5 6 7 8 9 0 - = {bksp}",
          "{tab} q w e r t y u i o p [ ] \\",
          "{lock} a s d f g h j k l ; ' {enter}",
          "{shift} z x c v b n m , . / {shift}",
          "{clear} {space} {close}"
        ],
        shift: [
          "~ ! @ # $ % ^ & * ( ) _ + {bksp}",
          "{tab} Q W E R T Y U I O P { } |",
          '{lock} A S D F G H J K L : " {enter}',
          "{shift} Z X C V B N M < > ? {shift}",
          "{clear} {space} {close}"
        ]
      },
      display: {
        '{bksp}': 'Back',
        '{close}': 'Close',
        '{enter}': 'Enter',
        '{clear}': 'Clear',
        '{tab}': 'Tab',
        '{lock}': 'Lock',
        '{shift}': 'Shift',
        '{space}': 'Space'
      },
      inputName: 'keyboardInput',
    });
    numKeyboard = new Keyboard('.numKeyboard', {
      onChange,
      onKeyPress,
      preventMouseDownDefault: true,
      layout: {
        default: ["1 2 3", "4 5 6", "7 8 9", "{clear} 0 ", "{bksp} {enter} {close}"],
        float: ["1 2 3", "4 5 6", "7 8 9", "0 {plusminus} .", "{bksp} {enter} {close}", "{clear}"]
      },
      display: {
        '{bksp}': 'Back',
        '{close}': 'Close',
        '{enter}': 'Enter',
        '{plusminus}': '+/-',
        '{clear}': 'Clear'
      },
      theme: "hg-theme-default hg-layout-numeric numeric-theme",
      inputName: 'keyboardInput',
    });
    alphaKeyboard.setCaretPosition(0, 0);
    numKeyboard.setCaretPosition(0, 0);
    await tick();
    if (keyboardType === KeyboardTypes.Numeric) {
      numRef.focus();
      numKeyboard.setOptions({ layoutName: float ? 'float' : 'default' });
    } else {
      alphaRef.focus();
    }
  });

  async function onChange(val: string): Promise<void> {
    input = val;
    await tick();
    syncCaretPosition();
  }

  function syncCaretPosition() {
    let caretPosition = activeKeyboard.caretPosition;
    if (caretPosition === null) {
      caretPosition = start.length;
      activeKeyboard.setCaretPosition(start.length, start.length);
    }
    if (caretPosition !== undefined && inputRef?.setSelectionRange) {
      inputRef?.focus();
      inputRef?.setSelectionRange(caretPosition, caretPosition);
    }
  }

  function onKeyPress(button: string): void {
    if (button === '{shift}' || button === '{lock}') {
      handleShift();
    }
    switch (button) {
      case '{enter}':
        dispatch('result-available', input);
        clear();
        break;
      case '{close}':
        dispatch('close-keyboard');
        // fallthrough
      case '{clear}':
        clear();
        break;
      case '{plusminus}':
        if (input.startsWith('-')) {
          input = input.substring(1);
        } else {
          input = '-' + input;
        }
        break;
    }
  }

  function closeKeyboard(): void {
    clear();
    dispatch('close-keyboard');
  }

  function clear(): void {
    input = '';
    start = '';
  }

  function handleShift(): void {
    const currentLayout = activeKeyboard.options.layoutName;
    const shiftToggle = currentLayout === 'default' ? 'shift' : 'default';
    activeKeyboard.setOptions({
      layoutName: shiftToggle,
    });
  }

  function onInput(event: Event): void {
    activeKeyboard.setInput((event.target as HTMLInputElement).value);
  }

</script>

<div class:hidden={hidden} class="min-w-screen h-screen animated fadeIn faster fixed left-0 top-0 flex justify-center items-center inset-0 z-50 outline-none focus:outline-none">
  <div class="relative mx-auto my-auto rounded-md shadow-md bg-blue-400 text-white" class:alpha={keyboardType === KeyboardTypes.Alpha}>
    <div class="w-full px-3 py-2">{label}</div>
    <div class="rounded-md shadow-md rounded-t-none bg-white text-black p-4">
      <div class="w-full">
        <input
          name="Input"
          type="text"
          placeholder=" "
          bind:value={input}
          class="peer block text-lg w-full appearance-none focus:outline-none mb-2"
          bind:this={inputRef}
          on:input={onInput}
        />
      </div>
      <div class:hidden={hiddenAlpha} class="h-full">
        <div class="alphaKeyboard" bind:this={alphaRef}></div>
      </div>
      <div class:hidden={hiddenNum}>
        <div class="numKeyboard" bind:this={numRef}></div>
      </div>
    </div>
  </div>
</div>
<div class:hidden class="opacity-25 fixed inset-0 z-40 bg-black" />

<style lang="postcss">
  .alpha {
    @apply w-1/2;
  }
</style>