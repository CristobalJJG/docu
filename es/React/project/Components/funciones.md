# Funciones Guays

## useEffect()
```js
useEffect(() => {
  // Código
}, [dependencias]);
```
Cuando se modifique `dependencia`, se ejecutarán las instrucciones dentro de `useEffect()`. Si `dependencia` es un array vacío, se ejecutará una sola vez.  

Por ejemplo:
```js
  useEffect(() => {
    searchOpen
      ? setAction({ method: METHODS.SEARCH, value: searchValue })
      : setAction({ method: METHODS.ANY, value: '' });
  }, [searchOpen]);
```

## useDispatch()
```js
const dispatch = useDispatch();

useEffect(() => {
  dispatch(fetchDependencia());
}, [dependencias]);
```
Por lo general (y lo que he visto en aplicacion), se suele utilizar para ejecutar las funciones de `fetch` de un **Slice de Redux**, con la intencion de hacer una llamada a una **API**, o con la intencion de setear una variable.

Por ejemplo:
```js
useEffect(() => {
    if(searchValue !== '' && 
            searchValue &&
            detailItems.length >= 1 ) {
        dispatch(setDetailItem(detailItems[0].id));
    }
}, [detailItems]);
```

## useSelector()
```js
const dependencia = useSelector((state) => state.reducer.dependencia);
```
Se utiliza para obtener el valor de una variable almacenada en el **Store de Redux**. Se le pasa una función que recibe el estado y devuelve el valor de la variable que se necesita.

Por ejemplo:
```js
const searchOpen = useSelector((state) => state.search.searchOpen);
```