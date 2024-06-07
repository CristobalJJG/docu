# Slices

Las Slices son un *"servicio"* de Redux, que se encarga de manejar el estado de la aplicación. Este se divide en *"reductores"* y *"acciones"*. Los reductores son funciones que se encargan de modificar el estado de la aplicación, y las acciones son funciones que se encargan de enviar información a los reductores.

## Estructura

Para tener un minimo control sobre cada slice deberiamos tener una estructura bien definida, por ejemplo:

```js
import {
  transformDataFromApiSomething,
} from '*';

/* Funciones que hacen fetch o llamadas a APIS */
export const fetchSomething = () => {
  return async (dispatch) => {
    try {
      const response = await fetch('https://api.com/something');
      const data = await response.json();
      return data
    } catch (error) { console.error(error); }
  };
};

/* Terminan las funciones que hacen fetch */

/* Estado inicial del Slice */
const initialState = {
  status: STATUS.IDLE,
  items: [],
  error: {},
  /* 
   * Aqui dentro deberian estar todas las 
   * variables que deba tener el reductor, si 
   * luego se modifica en algun caso, añadiendo 
   * una nueva variable, esta deberia ir aqui 
   */
};

export const somethingSlice = createSlice({
    name: 'something',
    initialState,
  reducers: {
    resetChanges: () => initialState
  },
  extraReducers: (builder) => {
    builder
      .addCase(fetchSomething.pending, (state) => {
        state.status = STATUS.PENDING;
        state.error = initialState.error;
      })
      .addCase(fetchSomething.rejected, (state, action) => {
        state.status = STATUS.REJECTED;
        state.error = action.payload;
      })
      .addCase(fetchSomething.fulfilled, (state, action) => {
        state.status = STATUS.FULFILLED;
        const somethingItems = transformDataFromApi(action.payload);
        state.items = detailItems;
        state.itemsByBarcode = detailItemsByBarcode;
        state.error = initialState.error;
      })
    /* Deberia haber un caso por cada estado que exista */
  }
});
```

Las forma en la que aplicamos los Slices se puede complicar todo lo que queramos, pero siempre **deberíamos tener una buena estructura** con un mínimo de control sobre cada uno de ellos.

## Usos
El uso principal es tener **información** en un **estado global**, que se pueda acceder desde cualquier parte de la aplicación, y que se pueda modificar desde cualquier parte de la aplicación.

### Configuración global
Podriamos tener un Slice que contenga la informacion esencia, informacion del usuario (idioma, unidades, ubicacion, etc.), filtros generales(un objeto que contenga los distintos tipos de filtros), etc.

```js
export const fetchUser = createAsyncThunk('global/fetchUser', async () => {
  try {
    return await fetch('https://api.com/user').json();
  } catch (error) { return error; }
});
export const initialState = {
  user: {
    language: 'es',
    location: 'Spain',
    units: 'metric',
    username: 'defaultUser',
  },
  filters: {
    searchName: '',
    dateFrom: '',
    dateTo: '',
  }
};

export const globalSlice = createSlice({
  name: 'global',
  initialState,
  reducers: {
    /* Incluimos las funciones que nos permiten cambiar los datos */
    changeLanguage: (state, action) => {
      state.user.language = action.payload;
    },
    changeLocation: (state, action) => {
      state.user.location = action.payload;
    },
    changeUnits: (state, action) => {
      state.user.units = action.payload;
    },
    changeUsername: (state, action) => {
      state.user.username = action.payload;
    },
    changeSearchName: (state, action) => {
      state.filters.searchName = action.payload;
    },
    changeDateFrom: (state, action) => {
      state.filters.dateFrom = action.payload;
    },
    changeDateTo: (state, action) => {
      state.filters.dateTo = action.payload;
    },
  },
  extraReducers: (builder) => {
    /* Aqui podriamos añadir mas reductores */
    builder
      .addCase(fetchUser.pending, (state) => {
        state.logged = initialState.logged;
        state.user = initialState.user;
        state.error = initialState.error;
      })
      .addCase(fetchUser.rejected, (state, action) => {
        state.logged = initialState.logged;
        state.user = initialState.user;
        state.error = action.payload;
      })
      .addCase(fetchUser.fulfilled, (state, action) => {
        state.logged = true;
        state.user = action.payload;
        state.error = initialState.error;
      });
  }
});

export const { 
    changeLanguage, changeLocation, 
    changeUnits, changeUsername, 
    changeSearchName, changeDateFrom, 
    changeDateTo } = globalSlice.actions;

export default appContext.reducer;
```

De esta forma tenemos un Slice que contiene la información global de la aplicación, y que se puede modificar desde cualquier parte de la aplicación.