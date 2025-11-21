# 🌾✨ ANÁLISIS COMPLETO DEL PROYECTO — *My Reactive Farm*


## 🧩 1. **Diferencia entre un componente presentacional y uno de página**
**Componente de página:** `src/pages/Farm.jsx`
- Maneja estado, efectos y peticiones API.
- Controla filtros, errores, loading.
- Contiene la lógica principal y la organización completa de la vista.

**Componentes presentacionales:** `AnimalForm`, `AnimalList`, `AnimalCard`
- Solo muestran interfaz.
- Reciben datos por *props*.
- No manejan lógica del servidor.

> 🟦 *Ejemplo real:*  
**Farm.jsx = Página**  
**AnimalForm.jsx / AnimalList.jsx / AnimalCard.jsx = Presentacionales**

---

## ⚙️ 2. **¿Para qué se usa useState en el proyecto?**
### Ejemplos reales:
- `const [animals, setAnimals] = useState([])` → Guarda lista de animales desde MockAPI.
- `const [typeFilter, setTypeFilter] = useState("all")` → Controla el filtro por tipo.

### Otros estados usados:
- `loading`
- `loadError`
- `submitError`
- `query`
- `statusFilter`

---

## 🔄 3. **¿Cómo se usa useEffect para cargar datos al inicio?**
**Flujo del proyecto:**
1. Al montar la página, se ejecuta el `useEffect`.
2. Llama a `getAnimals()` desde `animalsApi.js`.
3. Mientras carga: `setLoading(true)`.
4. Si llega la data: `setAnimals(data)`.
5. Si ocurre error: `setLoadError("Failed to load animals...")`.
6. Al terminar: `setLoading(false)`.

---

## 🚦 4. **Manejo de loading, error y lista vacía**
### ⏳ Loading
```jsx
{loading && <Loader message="Fetching animals..." />}
```

### ❌ Error
```jsx
{loadError && <Alert variant="error">{loadError}</Alert>}
```

### 📭 Lista vacía
Se muestra desde `AnimalList` (mensaje: "No animals found").

---

## 📝 5. **¿Qué es un formulario controlado en React?**
Es cuando el valor del input depende **del estado**, no del DOM.

Ejemplo real en el proyecto:
```jsx
value={values.name}
onChange={handleChange}
```
➡️ El input cambia solo si cambia el estado.

---

## 🗂️ 6. **¿Por qué separar la lógica en animalsApi.js?**
- Evita duplicar código.
- Mantiene la página limpia.
- Si cambia la URL de MockAPI, solo se actualiza un archivo.
- Facilita las pruebas.

---

## 🧱 7. **¿Por qué AnimalCard es reutilizable?**
- Recibe datos por *props*.
- No depende de la página.
- Solo muestra UI.

➡️ Podría funcionar para tarjetas de productos, mascotas, usuarios, etc.

---

## ♿ 8. **Accesibilidad presente en el proyecto**
- `aria-invalid`, `aria-describedby` → Ayuda a lectores de pantalla.
- `label` + `htmlFor` → Conecta etiquetas correctamente.
- `sr-only` → Texto accesible sin afectar el diseño.

---

## 💡 9. **Antes de agregar una nueva funcionalidad, piensa en:**
- Qué datos necesito.
- Qué estados deben existir.
- Dónde debe vivir ese estado.
- Qué componentes lo necesitarán.
- Si requieres un `useEffect`.

> 🔑 *Regla React:* **UI = Estado + funciones puras**

---

## 🚀 10. **Conceptos de React que funcionan en cualquier app**
- `useState` → Formularios, toggles, filtros.
- `useEffect` → Cargar datos.
- Formularios controlados → Login, registro, edición.
- Servicios API → Fetch organizado.
- Componentes presentacionales → Reutilización.
- Manejo de loading/error → Estandarizado.
---


## **Actividad Rama 1:**
### **¿Que fue lo que cambio?**
Pues lo que se hizo fue cambiar la constante del archivo `Farm.jsx` de la carpeta `src/pages`. Y al cambiar el useState de `typeFilter el all` a `cow` pues al cargar la página, la lista ya no muestra todos los animales, si no los de tipo `cow`.

---

### 🔧 Actividad 2 — Nuevo filtro por edad
Estado agregado



> const [minAge, setMinAge] = useState("");


Control agregado en la UI

> Input numérico con value={minAge} y onChange={setMinAge}.

Lógica de filtrado

Filtra animales que tengan age >= minAge.

> const byMinAge = !minAge || a.age >= Number(minAge);

## Qué ocurre visualmente

Al escribir un número, la lista solo muestra animales con edad mayor o igual.
Si no hay coincidencias, aparece mensaje de lista vacía.

---

### 🔧 Actividad 3 — Mensaje de éxito

**¿Que hizo?**

* Limpiar el formulario al enviar

Evita que el usuario tenga que borrar manualmente los inputs.

Se implementó reiniciando el estado values después del onSubmit.

**Mostrar mensaje de éxito**

Proporciona feedback visual inmediato.

> Se implementó usando un estado successMessage que desaparece automáticamente.
