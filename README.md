# Ngrx-VSCode-Snippets
Some Visual Studio Code Ngrx snippets.

## Installation
First, copy the snippet from this repository.  

1. Go to the snippet in this repo (typescript.json) and then click the "Raw" button.

![Raw button](/assets/images/raw.png "Raw Button")

2. Copy the entire snippet json file

Now in Visual Studio Code, go to File --> Preferences --> User Snippets.

A selector will open asking for what language to select, enter 'typescript' and you'll open the ```typescript.json``` file.  If the file is blank, you can simply paste the entire snippet into the file and save it.

If you already have some code, then you'll want to add these snippets to the end of your snippets.  You'll have to copy just the Ngrx JSON object snippets, and NOT the outer object.  Then you can paste the code into your JSON file and save it.

Now you'll have these snippets available in your application.

## To Use
To use these snippets, it's best to first create the folder structure and the empty typescript files based on the folder structure shown below.  Once all the Ngrx files have been created, then you can open one up and enter the snippet code.

For example, to enter Ngrx actions, open the ```actions.ts``` file and start typing: ```ngrx-crud-actions```.  (You should have Emmet installed by default with VS Code which will make this work)

When you see the full named prefix, you can press ```Tab``` to complete the snippet.  It will be highlighted and flashing.  While it is flashing, enter the name of the model for this module.  For this example, I will have created a Customer object.

```typescript
export interface Customer {
    id: number;
    firstName: string;
    lastName: string;
    ...
}
```

Each snippet file will accept both the Pascal-cased model and the camel-cased model.  The Pascal-cased model will be first, so enter ```Customer```.  Then hit ```Tab```, to move to the next position for the camel-cased placeholder, and type ```customer```.  The finally, ```Tab``` to finish the process.

Your Ngrx Actions file should be 99% finished.  You will just need to bring in the import statements.

Continue this process in each of the Ngrx files to create the Ngrx files for the feature module.

### CAUTION!!!
When importing statements, if you select the "Import all ..." option, be careful that you check that the references are correct.  Depending on other packages you have in your project, there could be types that are named the same as Ngrx types, such as ```Action```.  This can be found also in various other packages, so you'll have to double check that your import references are correct.


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
