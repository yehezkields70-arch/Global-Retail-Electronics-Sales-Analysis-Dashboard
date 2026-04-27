# Global Retail Electronics Sales Analysis
 
> **End-to-end Business Intelligence Project** menggunakan Microsoft Power BI untuk analisis penjualan retail multichannel.

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-217346?style=for-the-badge&logo=microsoft&logoColor=white)
![Data Modeling](https://img.shields.io/badge/Data%20Modeling-FF6F00?style=for-the-badge)

---

## Project Overview

Project ini adalah analisis komprehensif terhadap data penjualan retail yang mencakup **Online** dan **Offline** channel. Dashboard ini dirancang untuk membantu stakeholders memahami:

- ✅ Profitabilitas produk dan brand
- ✅ Performa toko per wilayah
- ✅ Segmentasi dan demografi pelanggan
- ✅ Tren penjualan secara time-series
- ✅ Perbandingan efisiensi channel

---

## Business Problem

Perusahaan retail menghadapi kesulitan dalam:
- Memantau **profit margin** per produk secara real-time
- Mengidentifikasi **toko paling efisien** (revenue per m²)
- Memahami **perilaku pelanggan** berdasarkan demografi
- Membandingkan performa **Online vs Offline**

---

## Dataset

| Table | Type | Description |
|-------|------|-------------|
| **Sales** | Fact Table | Transaksi penjualan harian |
| **Products** | Dimension | Detail produk, kategori, brand, harga |
| **Stores** | Dimension | Lokasi toko, luas, tanggal pembukaan |
| **Customers** | Dimension | Data demografi pelanggan |

---

## Data Transformation (Power Query)

### Tipe Data Conversion
```
Order Date    → Date
Open Date     → Date
Unit Cost USD → Decimal Number (remove $)
Unit Price USD→ Decimal Number (remove $)
```

### Feature Engineering
| New Column | Logic |
|------------|-------|
| **Channel** | `IF StoreKey = 0 THEN "Online" ELSE "Offline"` |
| **Usia Pelanggan** | `2020 - YEAR(Birthday)` |
| **Kelompok Usia** | `Muda (<30)`, `Dewasa (30-50)`, `Senior (>50)` |

---

## DAX Measures

```dax
// Revenue & Cost
Total Revenue = SUMX(Sales, Sales[Quantity] * RELATED(Products[Unit Price USD]))
Total Cost = SUMX(Sales, Sales[Quantity] * RELATED(Products[Unit Cost USD]))

// Profitability
Gross Profit = [Total Revenue] - [Total Cost]
Profit Margin % = DIVIDE([Gross Profit], [Total Revenue])

// Order Metrics
Total Orders = DISTINCTCOUNT(Sales[Order Number])
Average Order Value = DIVIDE([Total Revenue], [Total Orders])
Total Quantity = SUM(Sales[Quantity])
```

---

## Data Model (Star Schema)

```
                    ┌─────────────┐
                    │  Date Table │
                    └──────┬──────┘
                           │
         ┌─────────────────┼─────────────────┐
         │                 │                 │
    ┌────┴────┐      ┌────┴────┐      ┌────┴────┐
    │Products │      │ Stores  │      │Customers│
    └────┬────┘      └────┬────┘      └────┬────┘
         │                │                │
         └────────────────┼────────────────┘
                          │
                    ┌─────┴─────┐
                    │   Sales   │
                    │  (Fact)   │
                    └───────────┘
```

---

## 📈 Dashboard Preview

### KPI Cards (Top Row)
- Total Revenue
- Gross Profit
- Total Orders
- verage Order Value

### Visualizations
| Chart Type | Purpose |
|------------|---------|
| **Line Chart** | Revenue trend per bulan & tahun |
| **Map** | Revenue distribution per negara |
| **Donut Chart** | Revenue composition per kategori |
| **Horizontal Bar** | Top 10 produk terlaris |
| **Clustered Bar** | Online vs Offline comparison |
| **Scatter Plot** | Revenue vs Profit Margin per brand |
| **Treemap** | Distribusi pelanggan per negara |

### Slicers/Filters
- Tahun
- Negara
- Kategori
- Channel

---

## Key Insights

- 📌 **High-Volume Low-Margin Products**: Identifikasi produk dengan penjualan tinggi tapi margin rendah
- 📌 **Store Efficiency**: Analisis revenue per m² untuk optimasi toko
- 📌 **Customer Segmentation**: Pemahaman demografi pelanggan berdasarkan usia & gender
- 📌 **Channel Performance**: Perbandingan kontribusi Online vs Offline

---

## Tools & Technologies

- **Microsoft Power BI Desktop**
- **Power Query** (ETL)
- **DAX** (Data Analysis Expressions)
- **Star Schema Data Modeling**
- **Time Intelligence**

---

## Project Files

```
📦 Global-Retail-Electronics-Sales-Analysis/
│
├── 📄 README.md                    
├── 📁 docs/                       
│   ├── 01_Project_Brief.txt
│   ├── 02_PowerQuery_Transformation_Guide.txt
│   ├── 03_DAX_Measures_Documentation.txt
│   ├── 04_Dashboard_Layout_Guide.txt
│   └── 05_Project_Index.txt
│
├── 📁 data/                       
│   ├── Sales.csv
│   ├── Products.csv
│   ├── Stores.csv
│   └── Customers.csv
│
├── 📁 images/                      
│   ├── dashboard_overview.png
│   ├── product_analysis.png
│   ├── store_analysis.png
│   └── customer_analysis.png
│
└── 📊 Global_Retail_Electronics.pbix   
```
---

## How to Use

1. Download file `.pbix`
2. Buka di **Power BI Desktop**
3. Interaksi dengan slicers untuk filter data
4. Klik visual untuk cross-filtering

---

## Contact

-- Yehezkiel Destianto Saputra - Data Analyst  
📧 yehezkields70@gmail.com  
💼 [LinkedIn](https://www.linkedin.com/in/yehezkiel-destianto-saputra-37185a38a)


