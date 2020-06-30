# Ngrx-VSCode-Snippets
Some Visual Studio Code Ngrx snippets.

## Ngrx Snippets
There are full CRUD snippets for all the Ngrx operations (actions, reducer, effects, selectors).  These were created based on best practices and conventions.

There might be some adjustment in some import paths to other Ngrx operations, but they should be easily updated.

These are the proposed guidelines for the application structure and placement of your Ngrx operations.

```
src
  app
    customer
      _ngrx
        customer.action-types.ts
        customer.actions.ts
        customer.effects.ts
        customer.reducer.ts
        customer.selectors.ts
      customer-routing.module.ts
      customer.component.ts
      customer.module.ts
    core
      reducer
        index.ts  <-- application wide Ngrx reducers
```

In your ```customer.module.ts``` you can now add your Ngrx modules.

```typescript
@NgModule({
    imports: [
        ...
        StoreModule.forFeature('customers', customerReducer),
        EffectsModule.forFeature([CustomerEffects])
        ...
    ]
})
export class CustomerModule() {}
```

In your application wide Ngrx reducer file (index.ts), you would add the following code:

```typescript
import { ActionReducerMap, MetaReducer } from '@ngrx/store';
import { routerReducer } from '@ngrx/router-store';

export interface AppState {}

export const reducers: ActionReducerMap<AppState> = { router: routerReducer };
export const metaReducers: Array<MetaReducer<AppState>> = [];
```
