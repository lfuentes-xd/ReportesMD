
<h1>Reporte Número 2</h1>

<center>

## Mejorando la parte visual y las graficas

</center>

----

#### ¿qué es tailwind css? 


![logo de tailwind css](../Reportes/Imagenes/Tailwind_CSS_Logo.jpg)

tailwind es una Library de css de codigo abierto muy ampliamente usada en todo el mundo por su versatilidad y por ser diferemte a Boostrap, que tiene estilos ya predefinidos o componentes ya hechos por lo que los sitios hechos con boostrap son muy similares entre si, a diferencia de tailwind con el que podemos crear nuestros propios estilos. 

```HTML
<div class="bg-white dark:bg-slate-800 rounded-lg px-6 py-8 ring-1 ring-slate-900/5 shadow-xl">
  <div>
    <span class="inline-flex items-center justify-center p-2 bg-indigo-500 rounded-md shadow-lg">
      <svg class="h-6 w-6 text-white" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor" aria-hidden="true"><!-- ... --></svg>
    </span>
  </div>
  <h3 class="text-slate-900 dark:text-white mt-5 text-base font-medium tracking-tight">Writes Upside-Down</h3>
  <p class="text-slate-500 dark:text-slate-400 mt-2 text-sm">
    The Zero Gravity Pen can be used to write in any orientation, including upside-down. It even works in outer space.
  </p>
</div>
```

### ¿entonces cual son las ventajas de usar tailwind  ? 

1. Flujo de trabajo rapido 
2. Personalizable y escalable
3. Buena optimizacion 
4. Componentes
5. Aprendizaje rapido
6. Documetacion y comunidad oficial
7. Integracion con muchos frameworks

es mas sencillo pues hace uso de palabras clave, que representan muchas mas lineas en Css puro, como por ejemplo 

```css
mx-auto 
bg-red-500
```
en Css seria. 


```css
.element {
  margin-left: auto;
  margin-right: auto;
}
.element {
  background-color: #f56565;
}
```
y asi hay muchos otros...

### ¿pero si se puede usar ? 

para nuestro caso si. 
pues tiene licensia MIT
[link aqui](https://github.com/tailwindlabs/tailwindcss/blob/next/LICENSE)


----

### Mejora de la estrucutra y orgranizacion del backend

se decidió mejorar la estructura de las carpetas dentro del proyecto de flask, para tener
una mejor organización dentro del mismo, dejandolo así. 


- .Venv
- src
  - globalInfo
  - __init__.py
  -apartments.json
  -datos.json
  functions.py
- main.py

asi se tiene una mejor organizaicon dentro de los archivos. 

pues dentro de Main, se tiene asi una mejor estructura y orgranizaicon. 

```py
from flask import Flask, json, jsonify
from flask_cors import CORS
import src.functions as functions
import src.GlobalInfo.Messages as Messages

app = Flask(__name__)
CORS(app) 


@app.route("/AveragePrices", methods=["GET"])
def getApartmentsPrices():
    try:
        print("getting into Apartments pricing")
        objResult = functions.Apartmentsprices()
        return objResult
    except Exception as e :
        print("error while getting the prices and the m2 of the apartments... check this out:", e)
        return jsonify(Messages.err500)


@app.route("/BicepsAnalisis", methods=["GET"])
def getBicepsAnalisis():
    try:
        print("getting into analisis")
        objResult = functions.BicepsAnalysis()
        return objResult
    except Exception as e :
        print("erroren while getting the analisis:", e)
        return jsonify(Messages.err500)
```

y asi separamos las funciones de las rutas. 

por ejemplo en functions se tienen estos procesos...

```py

def WeigthAnalysis():
    try:
        with open('src/datos.json') as json_file:
             data = json.load(json_file) 

        weigth_analysis = {
            "Hombres":{
                "total": 0,
                "peso_total": 0,
                "peso_min": float('inf'),
                "peso_max": float('-inf')
            }, 
            "Mujeres":{
                "total": 0,
                "peso_total": 0,
                "peso_min": float('inf'),
                "peso_max": float('-inf')
            }
        }

        
        for item in data: 
            if item["sexo"] == "Hombre": 
                weigth_analysis["Hombres"]["total"] += 1
                weigth_analysis["Hombres"]["peso_total"] += item["peso"]
                weigth_analysis["Hombres"]["peso_min"] = min(weigth_analysis["Hombres"]["peso_min"], item["peso"])
                weigth_analysis["Hombres"]["peso_max"] = max(weigth_analysis["Hombres"]["peso_max"], item["peso"])
            elif item["sexo"] == "Mujer":
                weigth_analysis["Mujeres"]["total"] += 1
                weigth_analysis["Mujeres"]["peso_total"] += item["peso"]
                weigth_analysis["Mujeres"]["peso_min"] = min(weigth_analysis["Mujeres"]["peso_min"], item["peso"])
                weigth_analysis["Mujeres"]["peso_max"] = max(weigth_analysis["Mujeres"]["peso_max"], item["peso"])

        weigth_analysis["Hombres"]["peso_promedio" ] = round(weigth_analysis["Hombres"]["peso_total"] / weigth_analysis["Hombres"]["total"], 2) if weigth_analysis["Hombres"]["total"] > 0 else 0
        weigth_analysis["Mujeres"]["peso_promedio"] = round(weigth_analysis["Mujeres"]["peso_total"] / weigth_analysis["Mujeres"]["total"], 2) if weigth_analysis["Mujeres"]["total"] > 0 else 0

        return jsonify(weigth_analysis)
    except Exception as e:
        return jsonify({"error": "Archivo no encontrado"}), 404
```

ademas se agrefo un archivo dentro de globalInfo para los mensajes de error...

```py
err500={'intResponse':'500','strAnswer':'Server Error.'}

err203={'intResponse':'203','strAnswer':'Wrong data.'}

err205={'intResponse':'205','strAnswer':'Invalid Token'}

succ200={'intResponse':'200','strAnswer':'Success request'}
```

asi podemos copiar los mensajes de error y evitar escribir codigo de mas...

### Mejora y adicion de nuevos graficos en react 

por parte de react se siguio casi con la misma estructura exceptuando la parte de las views, donde se decidio hacer una subcarpeta para poder así agrupar de mejor forma las vistas. algo asi ...

- Views
  - Weigth
    - Weigth1.tsx
    - Weigth2.tsx
    - Weigth3.tsx
    - index.ts
  - PrincipalWeigth.tsx

en el archivo index.ts se hizo un archivo de barril, esto para que al momento de pasar todas las graficas en una vista no se vieran desorganizadas las importaciones. 

```ts
export * from './BicepsWeight'
export * from './Graphics'
export * from './NormalWeight'
export * from './PieWeigth'
export * from './Weigth'	
export * from './WeigthAnalysis'
```

para que al momento de usarlas se vea asi ...

```tsx
import { BicepsWeight, Graphics, NormalWeight, WeigthAnalysis, PieWeigth, Weigth } from '../Views/Pesos/index'

export const Weights = () => {
    return (
        <>
            <Weigth />
            <NormalWeight />
            <WeigthAnalysis />
            <BicepsWeight />
            <Graphics />
            <PieWeigth />
        </>
    )
}
```

se mejorro tambien la barra de navegacion con algunos estilos css...

```css
.header {
    background-color: #1e293b;
}

.containerPadre {
    margin-right: auto;
    margin-left: auto;
    padding-top: 3rem;
    padding-bottom: 3rem;
    width: 100%;
}

.container {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.text {
    text-transform: uppercase;
    font-size: small;
    color: #fff;
    font-weight: 700;
}

.navb {
    display: flex;
    gap: 1rem;
    margin-left: auto;
    margin-right: auto;
}
```

lo que nos deja ver la barra de navegación así...

![Grafica usando la libreria Echart](../Reportes/Imagenes/navbar.png)

el mismo patron se siguio con la parte de los departamentos  dejando todas las graficas de los mismos en una carpeta con su propio archivo de barril, y renderizando todos ellos dentro de una misma view. algo asi. 

![Grafica usando la libreria Echart](../Reportes/Imagenes/Grphics.png)

adenmas se decidió hacder todo el procesamiento de los datos desde el backend para que el rendimiento del frontend sea mejor... para que asi se manden los datos ya procesados y listos solo para leerse en el frontend y asi tengamos una mejor visuzalicion de los datos. 
por ejemplo el siguiente metodo es para separar los datos en edades y hacer asi la relacion entre los biceps y la edad de las personas, posteriormente esos datos se leeran en el front (ya trnasformados) lo que acelerará el proceso de lectura y visuzalicion de los datos. 

```py
def weigth():
    try:
        with open('src/datos.json') as json_file:
            data = json.load(json_file) 
        age_groups = {
            "20-30": {"total": 0, "biceps": 0},
            "31-40": {"total": 0, "biceps": 0},
            "41-50": {"total": 0, "biceps": 0},
            "51+": {"total": 0, "biceps": 0},
        }

        for item in data: 
            if 20 <= item["edad"] <= 30:
                age_groups["20-30"]["total"] += 1
                age_groups["20-30"]["biceps"] += item["biceps"]
            elif 31 <= item["edad"] <= 40:
                age_groups["31-40"]["total"] += 1
                age_groups["31-40"]["biceps"] += item["biceps"]
            elif 41 <= item["edad"] <= 50:
                age_groups["41-50"]["total"] += 1
                age_groups["41-50"]["biceps"] += item["biceps"]
            else:
                age_groups["51+"]["total"] += 1
                age_groups["51+"]["biceps"] += item["biceps"]

        dataset_source = [
            ["Edad", "Promedio de bíceps", "Cantidad de personas"],
            ["20-30", round(age_groups["20-30"]["biceps"] / age_groups["20-30"]["total"], 2) if age_groups["20-30"]["total"] > 0 else 0, age_groups["20-30"]["total"]],
            ["31-40", round(age_groups["31-40"]["biceps"] / age_groups["31-40"]["total"], 2) if age_groups["31-40"]["total"] > 0 else 0, age_groups["31-40"]["total"]],
            ["41-50", round(age_groups["41-50"]["biceps"] / age_groups["41-50"]["total"], 2) if age_groups["41-50"]["total"] > 0 else 0, age_groups["41-50"]["total"]],
            ["51+", round(age_groups["51+"]["biceps"] / age_groups["51+"]["total"], 2) if age_groups["51+"]["total"] > 0 else 0, age_groups["51+"]["total"]]
        ]
        return jsonify(dataset_source)
    except Exception as e:
        return jsonify({"error": "Archivo no encontrado"}), 404
   
```

por ultimo se necesita subir los avances, dado que los proyectos son independientes a el repositorio donde se subiran se tendran que trabajar como submodulos de la siguiente manera. 

```git
git submodule add route file
```

algo asi ...

