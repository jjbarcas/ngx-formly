# @ngx-formly/optimus-ui

[Optimus UI](https://optimus.openng.org/) field types and wrappers for Formly. This adapter connects Optimus UI inputs, selection controls, and validation messages to Angular Reactive Forms.

Optimus UI is a community-maintained, MIT-licensed fork of PrimeNG. Its components keep the PrimeNG selectors and inputs, so this adapter mirrors [`@ngx-formly/primeng`](https://github.com/ngx-formly/ngx-formly/tree/main/src/ui/primeng).

## Installation

For Formly 11, use Angular 22 and Optimus UI 2.0.2 or newer. Keep all `@ngx-formly/*` packages on the same version, and use an `@angular/forms` version matching your application.

In an Angular application with Reactive Forms installed:

```sh
npm install @ngx-formly/core@^11 @ngx-formly/optimus-ui@^11 @openng/optimus-ui@^2.0.2 @openng/optimus-ui-themes@^2.0.2 @angular/cdk@^22
```

The example below configures the Aura theme. Keep your existing `provideOptimus()` configuration if the application already has one. See the [Optimus UI documentation](https://optimus.openng.org/) for the UI library's application setup requirements.

## Configuration

Add the adapter to your application providers in `app.config.ts`:

```ts
import { ApplicationConfig } from '@angular/core';
import { provideOptimus } from '@openng/optimus-ui/config';
import Aura from '@openng/optimus-ui-themes/aura';
import { provideFormlyCore } from '@ngx-formly/core';
import { withFormlyOptimusUI } from '@ngx-formly/optimus-ui';

export const appConfig: ApplicationConfig = {
  providers: [provideOptimus({ theme: { preset: Aura } }), provideFormlyCore(withFormlyOptimusUI())],
};
```

## Usage

This field renders an email input using Optimus UI:

```ts
import { Component } from '@angular/core';
import { FormGroup, ReactiveFormsModule } from '@angular/forms';
import { FormlyFieldConfig, FormlyForm } from '@ngx-formly/core';

@Component({
  selector: 'app-example',
  imports: [ReactiveFormsModule, FormlyForm],
  template: `
    <form [formGroup]="form">
      <formly-form [form]="form" [fields]="fields" [model]="model"></formly-form>
    </form>
  `,
})
export class ExampleComponent {
  form = new FormGroup({});
  model = { email: '' };
  fields: FormlyFieldConfig[] = [
    {
      key: 'email',
      type: 'input',
      props: { type: 'email', label: 'Email', required: true },
    },
  ];
}
```

## Field types

`withFormlyOptimusUI()` registers `input`, `textarea`, `checkbox`, `radio`, and `select`, together with their form-field wrapper.

The `datepicker` type is available separately from `@ngx-formly/optimus-ui/datepicker`. Import `withFormlyFieldDatepicker` from that entry point and replace the Formly provider above with:

```ts
provideFormlyCore([...withFormlyOptimusUI(), withFormlyFieldDatepicker()]);
```

Individual registrations are also available from entry points such as `@ngx-formly/optimus-ui/input` and `@ngx-formly/optimus-ui/select`.

## Which Version to use?

Match `@ngx-formly/optimus-ui` to your `@ngx-formly/core` version, and check the migration guide for UI library requirements.

| Angular version | Formly version                | Migration                                                                            |
| --------------- | ----------------------------- | ------------------------------------------------------------------------------------ |
| Angular >= 22   | `@ngx-formly/optimus-ui@11.x` | [Upgrade to v11](https://github.com/ngx-formly/ngx-formly/blob/main/UPGRADE-11.0.md) |

## Documentation

- [Optimus UI examples](https://formly.dev/ui/optimus-ui)
- [Formly guide](https://formly.dev/guide)
- [Source](https://github.com/ngx-formly/ngx-formly/tree/main/src/ui/optimus-ui)
