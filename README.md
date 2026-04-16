# Acti

# Identificación y Corrección de Bugs

## Bugs Encontrados y Soluciones

### 1. gastos_view.py – Error 1
**Tipo de error:** Lógica / Tipo de dato  
**Descripción:** El monto del gasto se manejaba como cadena de texto (string) en lugar de un valor numérico, lo que provocaba resultados incorrectos al realizar operaciones matemáticas.  
**Causa:** Se utilizaba directamente el valor sin conversión de tipo.

    total += gasto.monto

**Solución:** Convertir el valor a tipo numérico antes de operar.

    total += float(gasto.monto)

### 2. gastos_view.py – Error 2
**Tipo de error:** Flujo / Validación  
**Descripción:** No se validaban los datos ingresados, permitiendo registrar gastos con campos vacíos.  
**Causa:** Falta de validación antes de guardar los datos.  
**Solución:** Agregar una validación previa para asegurar que los campos estén completos.

    if not nombre or not monto:
        return

### 3. dashboard_view.py – Error 1
**Tipo de error:** Lógica  
**Descripción:** El total de gastos mostrado en el dashboard no se calculaba correctamente.  
**Causa:** No se recorría adecuadamente la lista de gastos o no se convertían los datos al tipo correcto.  
**Solución:** Recalcular el total utilizando una suma adecuada.

    total = sum(float(g.monto) for g in gastos)

### 4. dashboard_view.py – Error 2
**Tipo de error:** POO / Acceso a atributos  
**Descripción:** Se intentaba acceder a un atributo inexistente dentro del objeto gasto.  
**Causa:** Uso incorrecto del nombre del atributo.

    gasto.categoria_nombre

**Solución:** Acceder correctamente al atributo dentro del objeto relacionado.

    gasto.categoria.nombre

### 5. historial_view.py – Error 1
**Tipo de error:** Lógica (ordenamiento)  
**Descripción:** El historial de gastos no se mostraba en orden cronológico correcto.  
**Causa:** No se aplicaba ningún método de ordenamiento.  
**Solución:** Ordenar los registros por fecha en orden descendente.

    gastos.sort(key=lambda x: x.fecha, reverse=True)

### 6. historial_view.py – Error 2
**Tipo de error:** Tipo de dato / Formato  
**Descripción:** Las fechas se manejaban como cadenas de texto, lo que afectaba su correcta manipulación y ordenamiento.  
**Causa:** No se convertía la fecha a un formato adecuado.  
**Solución:** Convertir la cadena a un objeto de tipo fecha.

    from datetime import datetime
    gasto.fecha = datetime.strptime(gasto.fecha, "%Y-%m-%d")

## Conclusión
Los errores detectados estaban relacionados principalmente con el manejo de tipos de datos, validaciones y acceso a atributos dentro de objetos. Aunque son errores simples, su impacto afecta directamente la funcionalidad y precisión de la aplicación. Al corregirlos, se mejora la confiabilidad del sistema y la correcta visualización de la información.
