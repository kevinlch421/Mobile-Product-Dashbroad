# DAX Definitions for Mobile Product Dashboard

## Calculated Table: Company Model Summary
**Purpose**: Creates aggregated view of key metrics by company and model  
**Location**: Data model tables  
**Logic**:
```dax
Company Model Summary = 
SUMMARIZE(
    'Mobile Dataset',
    'Mobile Dataset'[Company Name],
    'Mobile Dataset'[Model Name],
    "Average Wt", AVERAGE('Mobile Dataset'[Numerical wt]),
    "Average Price USD", AVERAGE('Mobile Dataset'[Launch Price (USD)]),
    "Average RAM", AVERAGE('Mobile Dataset'[RAM (GB)])
```

## Calculated Columns

### 1. Full Model Identifier
**Purpose**: Creates unique device identifier for relationships  
**Table**: Mobile Dataset  
**Logic**:
```dax
Full Model Identifier = 
CONCATENATE(
    'Mobile Dataset'[Company Name],
    'Mobile Dataset'[Model Name]
)
```

### 2. Weight String Length
**Purpose**: Enables weight value extraction  
**Table**: Mobile Dataset  
**Logic**:
```dax
Weight String Length = 
LEN('Mobile Dataset'[Mobile Weight])
```

### 3. Display Name
**Purpose**: User-friendly device naming for visuals  
**Table**: Mobile Dataset  
**Logic**:
```dax
Display Name = 
CONCATENATE(
    CONCATENATE('Mobile Dataset'[Company Name], " - "),
    'Mobile Dataset'[Model Name]
)
```

### 4. Numerical Weight
**Purpose**: Converts text weight to numeric value  
**Table**: Mobile Dataset  
**Logic**:
```dax
Numerical wt = 
IF(
    'Mobile Dataset'[Weight String Length] = 4,
    LEFT('Mobile Dataset'[Mobile Weight], 3),
    LEFT('Mobile Dataset'[Mobile Weight], 5)
)
```
**Note**: Handles both "195g" and "0.195kg" formats
