# Project: Text-to-SQL vs Direct Table QA

## Experimental Setup
- **Model:** Qwen/Qwen2.5-Coder-7B-Instruct
- **Databases used:** ['concert_singer', 'pets_1']
- **Evaluated Questions:** 87

## Average Results
| Method          |   Cell Precision |   Cell Recall |   Tuple Cardinality |
|:----------------|-----------------:|--------------:|--------------------:|
| Text-to-SQL     |         0.963602 |       0.95977 |            0.981191 |
| Direct Table-QA |         0.600738 |       0.64589 |            0.689908 |

## Error Analysis Summary
- Cases where SQL was better: 40
- Cases where QA was better: 1
- Cases where both failed (Recall < 1): 5
