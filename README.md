# The Wealth Index (SDSN 2026)

Este repositorio contiene los **datos de salida** y el **código reproducible (Stata)** para construir el **Índice de Riqueza estilo DHS usando los **Censos de Población y Vivienda de Bolivia (2012 y 2024)**.

La construcción sigue la lógica del **[DHS Wealth Index](https://dhsprogram.com/topics/wealth-index/Index.cfm)**, que utiliza **Análisis de Componentes Principales (PCA)** sobre un conjunto de variables de activos y condiciones de vivienda para aproximar el **estatus económico** del hogar (no ingreso ni consumo).

### Contenido del Repositorio

* **Código reproducible:** Archivos .do de Stata para el procesamiento y cálculo del índice.
* **Quintiles de riqueza:** Bases de datos con la estratificación socioeconómica resultante.
* **Datos municipales:** Resultados del índice agregados a nivel geográfico municipal.

---

## Requisitos de software

Este proyecto fue desarrollado y probado en **[Stata 17](https://www.stata.com/stata17/)**. Se recomienda utilizar esta versión o una superior para asegurar la compatibilidad de los scripts.

---

## Metodología

El índice se construye con PCA aplicado a variables de activos y características del hogar. El flujo general (estilo DHS) es:

1. Selección de variables que reflejen bienestar material (vivienda, servicios, activos, etc.).
2. Transformación a indicadores (principalmente dummies) y armonización para que **2012 y 2024** queden con **los mismos nombres finales** de variables.
3. Consolidación a nivel hogar usando el identificador del hogar/vivienda.
4. Tratamiento de faltantes (según el criterio definido en el documento titulado Steps to constructing the new DHS Wealth Index).
5. Análisis de Componentes Principales.
6. Uso del **primer componente** como puntaje de riqueza.
7. Estandarización del puntaje (z-score).
8. Clasificación en **quintiles** (o deciles).
9. Agregación a nivel municipal.

---

## Datos fuente

Los insumos utilizados en este análisis provienen exclusivamente del **Censo de Población y Vivienda 2012 y 2024** de Bolivia.

Para acceder a los enlaces de descarga y documentación oficial, diríjase a la carpeta denominada `source-data` dentro de este repositorio, donde encontrará la información al respecto.

---

## Variables utilizadas 

Las variables finales (ya construidas como dummies/indicadores a nivel hogar) se agrupan en:

### Calidad de vivienda
- Material de piso
- Material de pared
- Material de techo
- Personas por dormitorio

### Servicios básicos
- Fuente de agua
- Tipo de sanitario
- Tipo de desagüe
- Energía eléctrica
- Combustible para cocinar

### Bienes durables
- Radio, TV, teléfono, computadora
- Bicicleta, motocicleta, vehículo
- Cuarto exclusivo para cocinar
- Carreta/carretón
- Bote/canoa/balsa

### Tenencia y trabajo del hogar
- Tenencia/propiedad de la vivienda
- Presencia de ayuda doméstica

## Codebook 

| Variable | Descripción |
|--------|------------|
| piso_*_hog | Material del piso |
| techo*_hog | Material del techo |
| pared*_hog | Material de las paredes |
| agua_*_hog | Fuente de agua |
| sanit*_hog | Tipo de servicio sanitario |
| desag_*_hog | Tipo de desagüe |
| elec*_hog | Fuente de electricidad |
| comb_*_hog | Combustible para cocinar |
| radio_hog | Tiene radio |
| tv_hog | Tiene televisor |
| telef_hog | Tiene teléfono |
| comput_hog | Tiene computadora |
| bici_hog | Tiene bicicleta |
| moto_hog | Tiene motocicleta |
| vehic_hog | Tiene vehículo |
| cocina_hog | Cocina exclusiva |
| carreta_hog | Tiene carreta |
| bote_hog | Tiene bote |
| vivprop_hog | Vivienda propia |
| hacin_viv | Hacinamiento |
| ayuda_dom_viv | Ayuda doméstica |

### Variables de salida

| Variable | Descripción |
|--------|------------|
| wealth_score | Puntaje bruto del PCA (primer componente) |
| wealth_z | Puntaje estandarizado del índice de riqueza |
| q_wealth | Quintil de riqueza (1 = más pobre, 5 = más rico) |
| mun | Código de municipio |
| hogares | Número de hogares |
| mean_wealth | Promedio del índice de riqueza (municipal) |
| q1_share | Proporción de hogares en el quintil más pobre |
| q5_share | Proporción de hogares en el quintil más rico |




