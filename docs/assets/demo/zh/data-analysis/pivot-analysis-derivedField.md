---
category: examples
group: data-analysis
title: 派生字段
cover: https://lf9-dp-fe-cms-tos.byteorg.com/obj/bit-cloud/VTable/preview/pivot-analysis-derivedField.png
link: data_analysis/pivot_table_dataAnalysis
option: PivotTable#dataConfig.derivedFieldRules
---

# 派生字段

透视分析表格数据数据过滤规则，在 dataConfig 中配置 derivedFieldRules。

## 关键配置

- `PivotTable`
- `columns`
- `rows`
- `indicators`
- `dataConfig` 配置数据规则，可选配置项

## 代码演示

```javascript livedemo template=vtable
let tableInstance;
fetch('https://lf9-dp-fe-cms-tos.byteorg.com/obj/bit-cloud/VTable/North_American_Superstore_data.json')
  .then(res => res.json())
  .then(data => {
    const option = {
      records: data,
      rows: [
        {
          dimensionKey: 'Category',
          title: 'Category',
          headerStyle: {
            textStick: true
          },
          width: 'auto'
        },
        {
          dimensionKey: 'Sub-Category',
          title: 'Sub-Catogery',
          headerStyle: {
            textStick: true
          },
          width: 'auto'
        }
      ],
      columns: [
        {
          dimensionKey: 'Year',
          title: 'Year',
          headerStyle: {
            textStick: true
          },
          width: 'auto'
        },
        {
          dimensionKey: 'Month',
          title: 'Month',
          headerStyle: {
            textStick: true
          },
          width: 'auto'
        }
      ],
      indicators: [
        {
          indicatorKey: 'Quantity',
          title: 'Quantity',
          width: 'auto',
          showSort: false,
          headerStyle: {
            fontWeight: 'normal'
          },
          style: {
            padding: [16, 28, 16, 28],
            color(args) {
              if (args.dataValue >= 0) return 'black';
              return 'red';
            }
          }
        },
        {
          indicatorKey: 'Sales',
          title: 'Sales',
          width: 'auto',
          showSort: false,
          headerStyle: {
            fontWeight: 'normal'
          },
          format: rec => {
            return '$' + Number(rec).toFixed(2);
          },
          style: {
            padding: [16, 28, 16, 28],
            color(args) {
              if (args.dataValue >= 0) return 'black';
              return 'red';
            }
          }
        },
        {
          indicatorKey: 'Profit',
          title: 'Profit',
          width: 'auto',
          showSort: false,
          headerStyle: {
            fontWeight: 'normal'
          },
          format: rec => {
            return '$' + Number(rec).toFixed(2);
          },
          style: {
            padding: [16, 28, 16, 28],
            color(args) {
              if (args.dataValue >= 0) return 'black';
              return 'red';
            }
          }
        }
      ],
      corner: {
        titleOnDimension: 'row',
        headerStyle: {
          textStick: true
        }
      },
      dataConfig: {
        derivedFieldRules: [
          {
            fieldName: 'Year',
            derivedFunc: VTable.DataStatistics.dateFormat('Order Date', '%y', true)
          },
          {
            fieldName: 'Month',
            derivedFunc: VTable.DataStatistics.dateFormat('Order Date', '%n', true)
          }
        ],
        sortRules: [
          {
            sortField: 'Month',
            sortBy: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec']
          }
        ]
      },
      widthMode: 'standard'
    };
    tableInstance = new VTable.PivotTable(document.getElementById(CONTAINER_ID), option);
    window['tableInstance'] = tableInstance;
  });
```
