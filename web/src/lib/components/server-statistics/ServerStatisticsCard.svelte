<script lang="ts">
  import { ByteUnit } from '$lib/utils/byte-units';
  import { Icon, Text } from '@immich/ui';

  interface Props {
    icon: string;
    title: string;
    value?: number;
    unit?: ByteUnit | undefined;
  }

  let { icon, title, value = undefined, unit = undefined }: Props = $props();

  const zeros = $derived(() => {
    if (value === undefined) {
      return '';
    }
    const maxLength = 13;
    const valueLength = value.toString().length;
    const zeroLength = maxLength - valueLength;

    return '0'.repeat(zeroLength);
  });
</script>

<div class="flex h-35 w-full flex-col justify-between rounded-3xl bg-subtle text-primary p-5">
  <div class="flex place-items-center gap-4">
    <Icon {icon} size="40" />
    <Text size="giant" fontWeight="medium">{title}</Text>
  </div>

  <div class="mx-auto font-mono text-2xl font-medium">
    {#if value === undefined}
      <div class="flex items-center justify-center h-8">
        <svg class="animate-spin h-6 w-6 text-gray-500" fill="none" viewBox="0 0 24 24">
          <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
          <path
            class="opacity-75"
            fill="currentColor"
            d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"
          ></path>
        </svg>
      </div>
    {:else}
      <span class="text-gray-300 dark:text-gray-600">{zeros()}</span><span>{value}</span>
      {#if unit}
        <code class="font-mono text-base font-normal">{unit}</code>
      {/if}
    {/if}
  </div>
</div>
