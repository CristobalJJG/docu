# Store.js

Este archivo es el encargado de crear el store de Redux, el cual es utilizado por toda la aplicación para manejar el estado global de todos los elementos que queramos almacenar.

```js
// Building storaged reducer
import { persistReducer } from "redux-persist";
import { default as changes } from "./Slices/changes/changesSlice";
import storage from "redux-persist/lib/storage";

// Exporting all reducers
import { configureStore } from "@reduxjs/toolkit"; 
import appContextReducer from "./Slices/appContext/appContextSlice";
import userContextReducer from "./Slices/userContext/userContextSlice";
import settingsContextReducer from "./Slices/settingsContext/settingsContextSlice";

import thunk from "redux-thunk";

import persistStore from "redux-persist/es/persistStore";

// Building storaged reducer
const persistConfigChanges = {
  key: "changes",
  storage,
};
const changesReducer = persistReducer(persistConfigChanges, changes);

// Exporting all reducers
const store = configureStore({
  reducer: {
    appContext: appContextReducer,
    userContext: userContextReducer,
    settingsContext: settingsContextReducer,  
  },
  middleware: (getDefaultMiddleware) =>
    getDefaultMiddleware({
      thunk: { extraArgument: thunk },
      serializableCheck: false,
    })
});
const persistor = persistStore(store);
export { store, persistor };
```
