# Datos de Regiones y Comunas de Chile

Este proyecto contiene información detallada sobre las regiones y comunas de Chile. Incluye datos sobre las regiones y las comunas asociadas a cada una, así como funciones para acceder a esa información.

## Estructura de los Datos

Cada región en Chile está representada por un objeto que contiene el nombre de la región y una lista de las comunas que la componen. A continuación, se muestra un ejemplo de la estructura de los datos:

```typescript
interface IChileData {
  region: string;
  comunas: string[];
}

const chileData: IChileData[] = [
  {
    region: "Región Metropolitana de Santiago",
    comunas: [
      "Cerrillos", "Cerro Navia", "Conchalí", "El Bosque", "Estación Central", 
      "Huechuraba", "Independencia", "La Cisterna", "La Florida", "La Granja", 
      "La Pintana", "La Reina", "Las Condes", "Lo Barnechea", "Lo Espejo", 
      "Lo Prado", "Macul", "Maipú", "Ñuñoa", "Pedro Aguirre Cerda", 
      "Peñalolén", "Providencia", "Pudahuel", "Quilicura", "Quinta Normal", 
      "Recoleta", "Renca", "Santiago", "San Joaquín", "San Miguel", 
      "San Ramón", "Vitacura", "Puente Alto", "Pirque", "San José de Maipo", 
      "Colina", "Lampa", "Tiltil", "San Bernardo", "Buin", "Calera de Tango", 
      "Paine", "Melipilla", "Alhué", "Curacaví", "María Pinto", "San Pedro", 
      "Talagante", "El Monte", "Isla de Maipo", "Padre Hurtado", "Peñaflor"
    ]
  },
  {
    region: "Tarapacá",
    comunas: [
      "Iquique", "Alto Hospicio", "Pozo Almonte", "Camiña", "Colchane", 
      "Huara", "Pica"
    ]
  },
  // Otros datos de regiones y comunas...
];
```


## Ejemplo de uso y salida de regiones()
```typescript
Funciones Disponibles
regiones()
Esta función devuelve un array de objetos con las regiones de Chile. Cada objeto contiene dos propiedades:

label: El nombre de la región.
value: El nombre de la región, que es el mismo en este caso.

const regiones = (): { label: string; value: string }[] => {
  return chileData.map((item) => ({
    label: item.region,
    value: item.region,
  }));
};
```

## Ejemplo de uso y salida de comunasForRegiones()
```typescript
Funciones Disponibles
comunasForRegiones(region: string)
Esta función devuelve un array de objetos con las comunas de una región específica. Recibe como parámetro el nombre de la región, y devuelve las comunas asociadas a esa región.

const comunasForRegiones = (region: string): { label: string; value: string }[] => {
  const regionEncontrada = chileData.find((item) => item.region === region);
  return regionEncontrada
    ? regionEncontrada.comunas.map((comuna) => ({
        label: comuna,
        value: comuna,
      }))
    : [];
};
```


## Ejemplo de uso en componente de React arrow functions
```typescript
import React, { useState } from 'react';
import { regiones, comunasForRegiones, allComunas } from './path/to/chileData'; // Asegúrate de usar la ruta correcta

const ChileDataComponent: React.FC = () => {
  const [selectedRegion, setSelectedRegion] = useState<string>('');
  const [comunas, setComunas] = useState<string[]>([]);

  const handleRegionChange = (event: React.ChangeEvent<HTMLSelectElement>) => {
    const region = event.target.value;
    setSelectedRegion(region);
    setComunas(comunasForRegiones(region)); // Cargar comunas según la región seleccionada
  };

  const allRegions = regiones();
  const allChileComunas = allComunas();

  return (
    <div>
      <h1>Regiones de Chile</h1>
      <select onChange={handleRegionChange} value={selectedRegion}>
        <option value="">Seleccionar Región</option>
        {allRegions.map((region) => (
          <option key={region.value} value={region.value}>
            {region.label}
          </option>
        ))}
      </select>

      {selectedRegion && (
        <div>
          <h2>Comunas en {selectedRegion}</h2>
          <ul>
            {comunas.map((comuna, index) => (
              <li key={index}>{comuna}</li>
            ))}
          </ul>
        </div>
      )}

      <h2>Todas las Comunas de Chile</h2>
      <ul>
        {allChileComunas.map((comuna, index) => (
          <li key={index}>{comuna}</li>
        ))}
      </ul>
    </div>
  );
};

export default ChileDataComponent;
```

## ¡Se Agradece Mucho Una Estrellita! 🌟

Si este proyecto te ha sido útil o te ha gustado, no dudes en darle una estrella ⭐️ en GitHub. ¡Tu apoyo nos motiva a seguir mejorando! 😊

[¡Dale una estrella aquí!](https://github.com/SHRicard/chile-regiones-comunas)

¡Gracias por contribuir al open-source! 🎉


