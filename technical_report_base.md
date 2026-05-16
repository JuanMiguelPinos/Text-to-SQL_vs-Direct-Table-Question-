# Proyecto: Text-to-SQL vs Direct Table QA

## Configuración Experimental
- **Modelo:** Qwen/Qwen2.5-Coder-7B-Instruct
- **Bases de datos utilizadas:** ['concert_singer', 'pets_1']
- **Nº de Preguntas Evaluadas:** 87

## Resultados Promedio
| Method          |   Cell Precision |   Cell Recall |   Tuple Cardinality |
|:----------------|-----------------:|--------------:|--------------------:|
| Text-to-SQL     |         0.963602 |       0.95977 |            0.981191 |
| Direct Table-QA |         0.600738 |       0.64589 |            0.689908 |

## Resumen para Análisis de Errores
- Casos donde SQL fue mejor: 40
- Casos donde QA fue mejor: 1
- Casos donde ambos fallaron (Recall < 1): 5
