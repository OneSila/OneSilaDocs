
# Wizard Component

## Overview
The `Wizard.vue` component facilitates creating multi-step processes, like forms or wizards.

## Properties
- `steps`: Array of objects defining each step with a `title` and a `name`.
- `allowNextStep`: Boolean indicating if navigating to the next step is allowed.

## Usage
```vue
const wizardSteps = [
  { title: t('products.products.labels.type.title'), name: 'typeStep' },
  { title: t('shared.labels.sku'), name: 'skuStep' },
  { title: t('settings.vatRates.title'), name: 'vatStep' }
];

<template>
<Wizard ref="wizardRef" :steps="wizardSteps" :allow-next-step="allowNextStep" @on-finish="handleFinish" @update-current-step="updateStep">
    <template #typeStep>
         <!-- Content for step 1-->
    </template>

    <template #skuStep>
         <!-- Content for step 2-->
    </template>

    <template #vatStep>
         <!-- Content for step 3-->
    </template>
</Wizard>
</template>
```

## Slots
- Content for each step should be provided in named slots corresponding to the step `name`.

## Exposed Methods
- `nextStep`: Function to move to the next step.
- `goToStep`: Function to jump to a specific step by index.

## Events
- `onFinish`: Emitted when the final step is reached.
- `onNextStep`, `onBack`, `updateCurrentStep`: Emitted during navigation between steps.