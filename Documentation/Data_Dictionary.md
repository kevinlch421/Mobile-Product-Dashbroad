# Data Dictionary: Mobile Product Specifications

| Column Name               | Description                                      | Data Type |
|---------------------------|--------------------------------------------------|-----------|
| **Company Name**          | Manufacturer of the mobile device                | Text      |
| **Model Name**            | Specific product model name                      | Text      |
| **Mobile Weight**         | Physical weight of the device                    | Text      |
| **RAM**                   | Device memory capacity                           | Number    |
| **Front Camera**          | Selfie camera specifications                     | Text      |
| **Back Camera**           | Primary/rear camera specifications               | Text      |
| **Processor**             | Chipset model and core configuration             | Text      |
| **Battery Capacity**      | Energy storage capacity of the battery           | Number    |
| **Screen Size**           | Display diagonal measurement                     | Number    |
| **Launched Price (Pakistan)** | Official release price in Pakistan             | Number    |
| **Launched Price (India)**| Official release price in India                  | Number    |
| **Launched Price (China)**| Official release price in China                  | Number    |
| **Launched Price (USA)**  | Official release price in United States          | Number    |
| **Launched Price (Dubai)**| Official release price in United Arab Emirates   | Number    |
| **Launched Year**         | Year of product release                          | Number    |

## Derived Columns on DAX Function
1. **Numerical Weight**  
   Extracted numeric weight value from Mobile Weight  
   `Numerical Weight = VALUE(SUBSTITUTE(SUBSTITUTE([Mobile Weight],"g",""),"kg",""))`

2. **Display Name**  
   Combined company and model for reporting  
   `Display Name = [Company Name] & " - " & [Model Name]`

3. **Primary Camera MP**  
   Extracted megapixel value from Back Camera  
   `Primary Camera MP = VALUE(LEFT([Back Camera], FIND("MP",[Back Camera])-1))`

4. **Release Era**  
   Categorizes devices by launch period  
   `Release Era = IF([Launched Year] < 2023, "Pre-2023", "2023+")`
