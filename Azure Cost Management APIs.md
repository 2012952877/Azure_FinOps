# 需求

比如10台VM

按用量付费，vm id+日期+金额

每一天花了多少钱

有一个api，可以传日期

精细到每一天的明细

# API文档

[Microsoft Cost Management REST APIs | Microsoft Learn](https://learn.microsoft.com/en-us/rest/api/cost-management/?view=rest-cost-management-2023-11-01)

# Global查看服务价格的API

[Azure Retail Prices REST API overview | Microsoft Learn](https://learn.microsoft.com/en-us/rest/api/cost-management/retail-prices/azure-retail-prices?view=rest-cost-management-2023-11-01)

Azure customers have been looking for a programmatic way to retrieve retail prices for all Azure services. Now you can use the Retail Rates Prices API to get retail prices for all Azure services. Previously, the only way that you could retrieve prices for Azure services was to either use the Azure Pricing Calculator or use the Azure portal. This API gives you an unauthenticated experience to get retail rates for all Azure services. Use the API to explore prices for Azure services against different regions and different SKUs. The programmatic API can also help you create your own tools for internal analysis and price comparison across SKUs and regions.

>The currency that Microsoft uses to price all Azure services is USD. Prices shown in USD currency are Microsoft retail prices. Other non-USD prices returned by the API are for your reference to help you estimate budget expenses.

# 中国查看服务价格的API

[Azure Retail Prices REST API for China | Microsoft Learn](https://learn.microsoft.com/en-us/rest/api/cost-management/retail-prices/azure-retail-prices-china?view=rest-cost-management-2023-11-01)

This API gives you an unauthenticated experience to get retail rates for all Azure services in China. Use the API to explore prices for Azure services in different regions and different SKUs. The API can also help you create your own tools for internal analysis and price comparison across SKUs and regions. *The information in this article covers information that applies only to the Azure Retail Prices API for use in China*.

Through the API response, you get a URL to download a CSV file that includes the retail rates for all Azure services in China.

Retail prices shown in this document are examples.

# 这是什么

[Resource Manager | Microsoft Learn](https://learn.microsoft.com/en-us/rest/api/cost-management/operation-groups?view=rest-cost-management-2023-11-01)

## 先试试这个：Generate Cost Details Report

[Generate Cost Details Report - REST API (Azure Cost Management) | Microsoft Learn](https://learn.microsoft.com/en-us/rest/api/cost-management/generate-cost-details-report?view=rest-cost-management-2023-11-01)

![image-20240321150303091](./Azure Cost Management APIs.assets/image-20240321150303091.png)

This API is the replacement for all previously release Usage Details APIs. Request to generate a cost details report for the provided **date range**, **billing period (Only enterprise customers)** or **Invoice Id** asynchronously at a certain scope. The initial call to request a report will return a 202 with a 'Location' and 'Retry-After' header. The 'Location' header will provide the endpoint to poll to get the result of the report generation. The 'Retry-After' provides the duration to wait before polling for the generated report. A call to poll the report operation will provide a 202 response with a 'Location' header if the operation is still in progress. Once the report generation operation completes, the polling endpoint will provide a 200 response along with details on the report blob(s) that are available for download. The details on the file(s) available for download will be available in the polling response body. To Understand cost details (formerly known as usage details) fields found in files ,see https://learn.microsoft.com/en-us/azure/cost-management-billing/automate/understand-usage-details-fields

此 API 是以前发布的所有使用情况详细信息 API 的替代项。 请求为提供的日期范围、计费周期 (仅在特定范围内异步) 或发票 ID 的企业客户生成成本详细信息报表。 请求报告的初始调用将返回带有“Location”和“Retry-After”标头的 202。 “Location”标头将提供用于轮询的终结点，以获取报表生成的结果。 “Retry-After”提供轮询生成的报表之前等待的持续时间。 如果操作仍在进行中，则轮询报表操作的调用将提供带有“Location”标头的 202 响应。 报告生成操作完成后，轮询终结点将提供 200 响应以及报表 blob (可供下载) 的详细信息。 轮询响应正文中将提供可供下载的文件 () 的详细信息。 若要了解成本详细信息 (以前称为使用情况详细信息) 在文件中找到的字段，请参阅 https://learn.microsoft.com/en-us/azure/cost-management-billing/automate/understand-usage-details-fields

# 在官方文档的引导下

![image-20240321151046951](./Azure Cost Management APIs.assets/image-20240321151046951.png)



### QueryDataset

查询中存在的数据的定义。

展开表

| 名称          | 类型                                                         | 说明                                                         |
| :------------ | :----------------------------------------------------------- | :----------------------------------------------------------- |
| aggregation   | <string, [QueryAggregation](https://learn.microsoft.com/zh-cn/rest/api/cost-management/query/usage?view=rest-cost-management-2023-11-01&tabs=HTTP#queryaggregation)> | 在查询中使用的聚合表达式字典。 字典中每个项的键是聚合列的别名。 查询最多可以有 2 个聚合子句。 |
| configuration | [QueryDatasetConfiguration](https://learn.microsoft.com/zh-cn/rest/api/cost-management/query/usage?view=rest-cost-management-2023-11-01&tabs=HTTP#querydatasetconfiguration) | 具有导出中数据的配置信息。 如果提供聚合和分组，将忽略配置。  |
| filter        | [QueryFilter](https://learn.microsoft.com/zh-cn/rest/api/cost-management/query/usage?view=rest-cost-management-2023-11-01&tabs=HTTP#queryfilter) | 在查询中使用的筛选器表达式。 请参阅查询 API REST 文档，了解如何正确设置筛选器的格式。 |
| granularity   | [GranularityType](https://learn.microsoft.com/zh-cn/rest/api/cost-management/query/usage?view=rest-cost-management-2023-11-01&tabs=HTTP#granularitytype) | 查询中行的粒度。                                             |
| grouping      | [QueryGrouping](https://learn.microsoft.com/zh-cn/rest/api/cost-management/query/usage?view=rest-cost-management-2023-11-01&tabs=HTTP#querygrouping)[] | 在查询中使用的按表达式分组的数组。 查询最多可以有 2 个 group by 子句。 |

### QueryDefinition

查询的定义。

展开表

| 名称       | 类型                                                         | 说明                                                         |
| :--------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| dataset    | [QueryDataset](https://learn.microsoft.com/zh-cn/rest/api/cost-management/query/usage?view=rest-cost-management-2023-11-01&tabs=HTTP#querydataset) | 具有此查询中数据的定义。                                     |
| timePeriod | [QueryTimePeriod](https://learn.microsoft.com/zh-cn/rest/api/cost-management/query/usage?view=rest-cost-management-2023-11-01&tabs=HTTP#querytimeperiod) | 具有为查询拉取数据的时间段。                                 |
| timeframe  | [TimeframeType](https://learn.microsoft.com/zh-cn/rest/api/cost-management/query/usage?view=rest-cost-management-2023-11-01&tabs=HTTP#timeframetype) | 为查询拉取数据的时间范围。 如果自定义，则必须提供特定的时间段。 |
| type       | [ExportType](https://learn.microsoft.com/zh-cn/rest/api/cost-management/query/usage?view=rest-cost-management-2023-11-01&tabs=HTTP#exporttype) | 查询的类型。                                                 |



![image-20240321154442661](./Azure Cost Management APIs.assets/image-20240321154442661.png)

# 配置方法

[Query - Usage - REST API (Azure Cost Management) | Microsoft Learn](https://learn.microsoft.com/zh-cn/rest/api/cost-management/query/usage?view=rest-cost-management-2023-11-01&tabs=HTTP#timeframetype)



![image-20240321232327256](./Azure Cost Management APIs.assets/image-20240321232327256.png)

![image-20240321232338942](./Azure Cost Management APIs.assets/image-20240321232338942.png)

> 应该用ServiceName

```
{
    "type": "Usage",
    "timeframe": "MonthToDate",
    "dataset": {
        "granularity": "Daily",
        "aggregation": {
            "totalCost": {
                "name": "PreTaxCost",
                "function": "Sum"
            }
        },
        "grouping": [
            {
                "type": "Dimension",
                "name": "MeterCategory"
            }
        ]
    }
}
```

```
POST https://management.azure.com//subscriptions/5b6655c9-e8d6-4f6b-a98e-589f99588eb6/providers/Microsoft.CostManagement/query?api-version=2023-11-01
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6IlhSdmtvOFA3QTNVYVdTblU3Yk05blQwTWpoQSIsImtpZCI6IlhSdmtvOFA3QTNVYVdTblU3Yk05blQwTWpoQSJ9.eyJhdWQiOiJodHRwczovL21hbmFnZW1lbnQuY29yZS53aW5kb3dzLm5ldCIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzYyMGEwY2IyLTBlYmMtNDBlYi05ZTA5LWFiNWEzMTQyZWRjYi8iLCJpYXQiOjE3MTEwMDYxNTUsIm5iZiI6MTcxMTAwNjE1NSwiZXhwIjoxNzExMDEwNDE0LCJhY3IiOiIxIiwiYWlvIjoiQVZRQXEvOFdBQUFBbUZqZDBWMDdjYjRPTzZSeXMwdVZ2OVNyRUkzOFY0MnRncmE5alRpeC9lSUl4VE1MMExkVDJJejNXOFUyTDZpVzNvb3l5bGlOcEc1WjhkWXA0RFNtQTNOOGJmcHBYRFI5N05wZDJqWmlHMzA9IiwiYW1yIjpbInB3ZCIsIm1mYSJdLCJhcHBpZCI6IjE4ZmJjYTE2LTIyMjQtNDVmNi04NWIwLWY3YmYyYjM5YjNmMyIsImFwcGlkYWNyIjoiMCIsImdyb3VwcyI6WyI5OTA3NTQyNi1iNGIyLTQ3MWEtYTQyNy0zODRhZjc4ZjY3N2UiXSwiaWR0eXAiOiJ1c2VyIiwiaXBhZGRyIjoiMjQwNDpmODAxOjgwNTA6Mzo4MGJlOjoxNTEiLCJuYW1lIjoiTVMtU3VwcG9ydCIsIm9pZCI6Ijk0NTI1NjIwLTBjMDUtNDVmMy04MGQxLWE3MDI0NGYwN2VmNyIsInB1aWQiOiIxMDAzMjAwMzE4ODY1MUFBIiwicmgiOiIwLkFUMEFzZ3dLWXJ3TzYwQ2VDYXRhTVVMdHkwWklmM2tBdXRkUHVrUGF3ZmoyTUJPaEFMay4iLCJzY3AiOiJ1c2VyX2ltcGVyc29uYXRpb24iLCJzdWIiOiJBMVhHd2RhaGFfWDI3ekpfa0EzSXdBd0k2SFdWc19fZUdoVVpCZ3k5T2xzIiwidGlkIjoiNjIwYTBjYjItMGViYy00MGViLTllMDktYWI1YTMxNDJlZGNiIiwidW5pcXVlX25hbWUiOiJtc3N1cHBvcnRAanRwb2MyMDIzb3V0bG9vay5vbm1pY3Jvc29mdC5jb20iLCJ1cG4iOiJtc3N1cHBvcnRAanRwb2MyMDIzb3V0bG9vay5vbm1pY3Jvc29mdC5jb20iLCJ1dGkiOiJ0X2dqOVJVdkYwU1BLS2FXd0FJYUFBIiwidmVyIjoiMS4wIiwid2lkcyI6WyI2MmU5MDM5NC02OWY1LTQyMzctOTE5MC0wMTIxNzcxNDVlMTAiLCIxM2JkMWM3Mi02ZjRhLTRkY2YtOTg1Zi0xOGQzYjgwZjIwOGEiXSwieG1zX3RjZHQiOjE3MDAzOTE1Mzl9.MXlZsp-KsRXn-PRRAj-jgtQFTTIBNWs6o3asARSGE82sYogCmMkrPn55rqeZfdEb_kxdK_7RfudbhlzESEcQYHljevvEUooDdf8oqYkUVaO-r3MeOTzapOI1vPaJJx7joMoRgUXwja-BDyog0sX4pVnS6gyqb1Qu6qbzvzj6uBYvXP_6MHbyZnjym96BehjoFqiHYyumYpO7ZkzUKu20VjorCeP85p0t6cjYipgN-YOBi0JyuCP8-PO4LxjuGanEwCANKWFkrmtN0Ukr3S2KQTdIRYXXi9p2M69Zjgq4DV4rz0Jkti3q6TtRMWmaaNGZoKPcHJjh2FsXw0XmQLos_w
Content-type: application/json


```

![image-20240321232421289](./Azure Cost Management APIs.assets/image-20240321232421289.png)

```
cache-control: no-cache
content-length: 17004
content-type: application/json; charset=utf-8
date: Thu, 21 Mar 2024 08:16:35 GMT
expires: -1
pragma: no-cache
session-id: 557d1d78-bb22-4037-af0c-fe18b8abd623
vary: Accept-Encoding
x-ms-client-request-id: 7c0ec32c-eae6-4675-92d7-a6fbeaeda825
x-ms-correlation-request-id: 281729a1-b972-4f5c-8099-52327d2ca81f
x-ms-ratelimit-remaining-subscription-resource-requests: 99
x-ms-request-id: 6d1a2161-b164-4506-9b24-3697a130aafd
x-ms-routing-request-id: SOUTHEASTASIA:20240321T081636Z:281729a1-b972-4f5c-8099-52327d2ca81f
x-powered-by: ASP.NET

```

```
{
  "id": "subscriptions/5b6655c9-e8d6-4f6b-a98e-589f99588eb6/providers/Microsoft.CostManagement/query/bc764dfa-3192-47a7-bf93-83613dd3a319",
  "name": "bc764dfa-3192-47a7-bf93-83613dd3a319",
  "type": "Microsoft.CostManagement/query",
  "location": null,
  "sku": null,
  "eTag": null,
  "properties": {
    "nextLink": null,
    "columns": [
      {
        "name": "PreTaxCost",
        "type": "Number"
      },
      {
        "name": "UsageDate",
        "type": "Number"
      },
      {
        "name": "MeterCategory",
        "type": "String"
      },
      {
        "name": "Currency",
        "type": "String"
      }
    ],
    "rows": [
      [
        15.096,
        20240301,
        "Application Gateway",
        "USD"
      ],
      [
        0.0275757548387097,
        20240301,
        "Azure DNS",
        "USD"
      ],
      [
        23.6280993450968,
        20240301,
        "Azure Database for MySQL",
        "USD"
      ],
      [
        16.4529870692372,
        20240301,
        "Azure Front Door Service",
        "USD"
      ],
      [
        0.00001632,
        20240301,
        "Bandwidth",
        "USD"
      ],
      [
        1.00931731456e-7,
        20240301,
        "Content Delivery Network",
        "USD"
      ],
      [
        0.00068085,
        20240301,
        "Key Vault",
        "USD"
      ],
      [
        0.511201161387889,
        20240301,
        "Load Balancer",
        "USD"
      ],
      [
        0.9889857880692,
        20240301,
        "NAT Gateway",
        "USD"
      ],
      [
        171.06901758667,
        20240301,
        "Storage",
        "USD"
      ],
      [
        0,
        20240301,
        "Unassigned",
        "USD"
      ],
      [
        11.5056,
        20240301,
        "VPN Gateway",
        "USD"
      ],
      [
        365.8074848654,
        20240301,
        "Virtual Machines",
        "USD"
      ],
      [
        2.55021601509163,
        20240301,
        "Virtual Network",
        "USD"
      ],
      [
        5.1,
        20240301,
        "Virtual WAN",
        "USD"
      ],
      [
        15.096,
        20240302,
        "Application Gateway",
        "USD"
      ],
      [
        0.0276260748387097,
        20240302,
        "Azure DNS",
        "USD"
      ],
      [
        0.000017,
        20240302,
        "Azure Data Factory v2",
        "USD"
      ],
      [
        23.6449977045968,
        20240302,
        "Azure Database for MySQL",
        "USD"
      ],
      [
        17.5255465221941,
        20240302,
        "Azure Front Door Service",
        "USD"
      ],
      [
        0.00001632,
        20240302,
        "Bandwidth",
        "USD"
      ],
      [
        0.0006732,
        20240302,
        "Key Vault",
        "USD"
      ],
      [
        0.511200010180287,
        20240302,
        "Load Balancer",
        "USD"
      ],
      [
        0.975460621304344,
        20240302,
        "NAT Gateway",
        "USD"
      ],
      [
        171.0278792173,
        20240302,
        "Storage",
        "USD"
      ],
      [
        0,
        20240302,
        "Unassigned",
        "USD"
      ],
      [
        11.5056,
        20240302,
        "VPN Gateway",
        "USD"
      ],
      [
        365.804116842,
        20240302,
        "Virtual Machines",
        "USD"
      ],
      [
        2.55032039264077,
        20240302,
        "Virtual Network",
        "USD"
      ],
      [
        5.1,
        20240302,
        "Virtual WAN",
        "USD"
      ],
      [
        15.096,
        20240303,
        "Application Gateway",
        "USD"
      ],
      [
        0.0277199148387097,
        20240303,
        "Azure DNS",
        "USD"
      ],
      [
        0.000017,
        20240303,
        "Azure Data Factory v2",
        "USD"
      ],
      [
        20.0752758615968,
        20240303,
        "Azure Database for MySQL",
        "USD"
      ],
      [
        16.8286346191841,
        20240303,
        "Azure Front Door Service",
        "USD"
      ],
      [
        0.00001632,
        20240303,
        "Bandwidth",
        "USD"
      ],
      [
        0.0006732,
        20240303,
        "Key Vault",
        "USD"
      ],
      [
        0.511200004959526,
        20240303,
        "Load Balancer",
        "USD"
      ],
      [
        0.958479150669649,
        20240303,
        "NAT Gateway",
        "USD"
      ],
      [
        171.0278135449,
        20240303,
        "Storage",
        "USD"
      ],
      [
        0,
        20240303,
        "Unassigned",
        "USD"
      ],
      [
        11.5056,
        20240303,
        "VPN Gateway",
        "USD"
      ],
      [
        365.81088,
        20240303,
        "Virtual Machines",
        "USD"
      ],
      [
        2.55040234198049,
        20240303,
        "Virtual Network",
        "USD"
      ],
      [
        5.1,
        20240303,
        "Virtual WAN",
        "USD"
      ],
      [
        15.096,
        20240304,
        "Application Gateway",
        "USD"
      ],
      [
        0.0276563348387097,
        20240304,
        "Azure DNS",
        "USD"
      ],
      [
        0.000017,
        20240304,
        "Azure Data Factory v2",
        "USD"
      ],
      [
        20.0697448815968,
        20240304,
        "Azure Database for MySQL",
        "USD"
      ],
      [
        16.7901112570802,
        20240304,
        "Azure Front Door Service",
        "USD"
      ],
      [
        0.00001632,
        20240304,
        "Bandwidth",
        "USD"
      ],
      [
        0.000001413044240384,
        20240304,
        "Content Delivery Network",
        "USD"
      ],
      [
        0.0006732,
        20240304,
        "Key Vault",
        "USD"
      ],
      [
        0.511220788838854,
        20240304,
        "Load Balancer",
        "USD"
      ],
      [
        0.959902924651746,
        20240304,
        "NAT Gateway",
        "USD"
      ],
      [
        183.043264846987,
        20240304,
        "Storage",
        "USD"
      ],
      [
        0,
        20240304,
        "Unassigned",
        "USD"
      ],
      [
        11.5056,
        20240304,
        "VPN Gateway",
        "USD"
      ],
      [
        398.424491345,
        20240304,
        "Virtual Machines",
        "USD"
      ],
      [
        2.55048109461507,
        20240304,
        "Virtual Network",
        "USD"
      ],
      [
        5.1,
        20240304,
        "Virtual WAN",
        "USD"
      ],
      [
        11.1759322222222,
        20240305,
        "Application Gateway",
        "USD"
      ],
      [
        0.0276964548387097,
        20240305,
        "Azure DNS",
        "USD"
      ],
      [
        0.000017,
        20240305,
        "Azure Data Factory v2",
        "USD"
      ],
      [
        20.0536670520968,
        20240305,
        "Azure Database for MySQL",
        "USD"
      ],
      [
        16.7486622426688,
        20240305,
        "Azure Front Door Service",
        "USD"
      ],
      [
        0.00001632,
        20240305,
        "Bandwidth",
        "USD"
      ],
      [
        0.0006528,
        20240305,
        "Key Vault",
        "USD"
      ],
      [
        0.511248418925609,
        20240305,
        "Load Balancer",
        "USD"
      ],
      [
        1.02433124284283,
        20240305,
        "NAT Gateway",
        "USD"
      ],
      [
        195.113002637459,
        20240305,
        "Storage",
        "USD"
      ],
      [
        0,
        20240305,
        "Unassigned",
        "USD"
      ],
      [
        11.5056,
        20240305,
        "VPN Gateway",
        "USD"
      ],
      [
        448.7601457959,
        20240305,
        "Virtual Machines",
        "USD"
      ],
      [
        2.55060877287015,
        20240305,
        "Virtual Network",
        "USD"
      ],
      [
        5.1,
        20240305,
        "Virtual WAN",
        "USD"
      ],
      [
        14.1839429589685,
        20240306,
        "Application Gateway",
        "USD"
      ],
      [
        0.0276597348387097,
        20240306,
        "Azure DNS",
        "USD"
      ],
      [
        20.0607904680968,
        20240306,
        "Azure Database for MySQL",
        "USD"
      ],
      [
        17.0685600392149,
        20240306,
        "Azure Front Door Service",
        "USD"
      ],
      [
        11.0999685129544,
        20240306,
        "Bandwidth",
        "USD"
      ],
      [
        5.0465865728e-8,
        20240306,
        "Content Delivery Network",
        "USD"
      ],
      [
        0.00078795,
        20240306,
        "Key Vault",
        "USD"
      ],
      [
        0.511217556902487,
        20240306,
        "Load Balancer",
        "USD"
      ],
      [
        0.970209676607978,
        20240306,
        "NAT Gateway",
        "USD"
      ],
      [
        196.377775848338,
        20240306,
        "Storage",
        "USD"
      ],
      [
        0,
        20240306,
        "Unassigned",
        "USD"
      ],
      [
        11.5056,
        20240306,
        "VPN Gateway",
        "USD"
      ],
      [
        458.1186143121,
        20240306,
        "Virtual Machines",
        "USD"
      ],
      [
        2.4725012316207,
        20240306,
        "Virtual Network",
        "USD"
      ],
      [
        5.1,
        20240306,
        "Virtual WAN",
        "USD"
      ],
      [
        13.4233333747646,
        20240307,
        "Application Gateway",
        "USD"
      ],
      [
        0.0276315148387097,
        20240307,
        "Azure DNS",
        "USD"
      ],
      [
        0.000017,
        20240307,
        "Azure Data Factory v2",
        "USD"
      ],
      [
        20.0553916845968,
        20240307,
        "Azure Database for MySQL",
        "USD"
      ],
      [
        16.9485922549493,
        20240307,
        "Azure Front Door Service",
        "USD"
      ],
      [
        1.88046208469622,
        20240307,
        "Bandwidth",
        "USD"
      ],
      [
        0.000001148366880768,
        20240307,
        "Content Delivery Network",
        "USD"
      ],
      [
        0.00060435,
        20240307,
        "Key Vault",
        "USD"
      ],
      [
        0.511200084379222,
        20240307,
        "Load Balancer",
        "USD"
      ],
      [
        0,
        20240307,
        "Log Analytics",
        "USD"
      ],
      [
        1.42913502340321,
        20240307,
        "NAT Gateway",
        "USD"
      ],
      [
        198.392860626476,
        20240307,
        "Storage",
        "USD"
      ],
      [
        0.00553722446236561,
        20240307,
        "Traffic Manager",
        "USD"
      ],
      [
        0,
        20240307,
        "Unassigned",
        "USD"
      ],
      [
        11.5056,
        20240307,
        "VPN Gateway",
        "USD"
      ],
      [
        441.70813432418,
        20240307,
        "Virtual Machines",
        "USD"
      ],
      [
        2.44954450734984,
        20240307,
        "Virtual Network",
        "USD"
      ],
      [
        5.1,
        20240307,
        "Virtual WAN",
        "USD"
      ],
      [
        13.0639395762712,
        20240308,
        "Application Gateway",
        "USD"
      ],
      [
        0.0277549348387097,
        20240308,
        "Azure DNS",
        "USD"
      ],
      [
        0.000017,
        20240308,
        "Azure Data Factory v2",
        "USD"
      ],
      [
        20.0489140560968,
        20240308,
        "Azure Database for MySQL",
        "USD"
      ],
      [
        16.708673917563,
        20240308,
        "Azure Front Door Service",
        "USD"
      ],
      [
        1.59527558213268,
        20240308,
        "Bandwidth",
        "USD"
      ],
      [
        1.00931731456e-7,
        20240308,
        "Content Delivery Network",
        "USD"
      ],
      [
        0.0007752,
        20240308,
        "Key Vault",
        "USD"
      ],
      [
        0.511217947529443,
        20240308,
        "Load Balancer",
        "USD"
      ],
      [
        0,
        20240308,
        "Log Analytics",
        "USD"
      ],
      [
        0.97735920346342,
        20240308,
        "NAT Gateway",
        "USD"
      ],
      [
        199.1448818499,
        20240308,
        "Storage",
        "USD"
      ],
      [
        0.00987142674193551,
        20240308,
        "Traffic Manager",
        "USD"
      ],
      [
        0,
        20240308,
        "Unassigned",
        "USD"
      ],
      [
        11.5056,
        20240308,
        "VPN Gateway",
        "USD"
      ],
      [
        457.50174947674,
        20240308,
        "Virtual Machines",
        "USD"
      ],
      [
        2.45804321993142,
        20240308,
        "Virtual Network",
        "USD"
      ],
      [
        5.1,
        20240308,
        "Virtual WAN",
        "USD"
      ],
      [
        13.0622215677966,
        20240309,
        "Application Gateway",
        "USD"
      ],
      [
        0.0278079748387097,
        20240309,
        "Azure DNS",
        "USD"
      ],
      [
        0.000017,
        20240309,
        "Azure Data Factory v2",
        "USD"
      ],
      [
        20.0682724860968,
        20240309,
        "Azure Database for MySQL",
        "USD"
      ],
      [
        16.9088964580674,
        20240309,
        "Azure Front Door Service",
        "USD"
      ],
      [
        0.545140508834801,
        20240309,
        "Bandwidth",
        "USD"
      ],
      [
        4.677219385344e-7,
        20240309,
        "Content Delivery Network",
        "USD"
      ],
      [
        0.0006732,
        20240309,
        "Key Vault",
        "USD"
      ],
      [
        0.511200008426839,
        20240309,
        "Load Balancer",
        "USD"
      ],
      [
        0,
        20240309,
        "Log Analytics",
        "USD"
      ],
      [
        0.974404635761864,
        20240309,
        "NAT Gateway",
        "USD"
      ],
      [
        199.170161341,
        20240309,
        "Storage",
        "USD"
      ],
      [
        0.00987188574193551,
        20240309,
        "Traffic Manager",
        "USD"
      ],
      [
        0,
        20240309,
        "Unassigned",
        "USD"
      ],
      [
        11.5056,
        20240309,
        "VPN Gateway",
        "USD"
      ],
      [
        469.07134247376,
        20240309,
        "Virtual Machines",
        "USD"
      ],
      [
        2.44839879059605,
        20240309,
        "Virtual Network",
        "USD"
      ],
      [
        5.1,
        20240309,
        "Virtual WAN",
        "USD"
      ],
      [
        13.0619734110169,
        20240310,
        "Application Gateway",
        "USD"
      ],
      [
        0.0278093348387097,
        20240310,
        "Azure DNS",
        "USD"
      ],
      [
        0.000017,
        20240310,
        "Azure Data Factory v2",
        "USD"
      ],
      [
        20.0600003280968,
        20240310,
        "Azure Database for MySQL",
        "USD"
      ],
      [
        17.4067112216896,
        20240310,
        "Azure Front Door Service",
        "USD"
      ],
      [
        0.542270534521497,
        20240310,
        "Bandwidth",
        "USD"
      ],
      [
        0.0006732,
        20240310,
        "Key Vault",
        "USD"
      ],
      [
        0.511200001060776,
        20240310,
        "Load Balancer",
        "USD"
      ],
      [
        0,
        20240310,
        "Log Analytics",
        "USD"
      ],
      [
        0.972493564076722,
        20240310,
        "NAT Gateway",
        "USD"
      ],
      [
        199.1701409734,
        20240310,
        "Storage",
        "USD"
      ],
      [
        0.00987096774193551,
        20240310,
        "Traffic Manager",
        "USD"
      ],
      [
        0,
        20240310,
        "Unassigned",
        "USD"
      ],
      [
        11.5056,
        20240310,
        "VPN Gateway",
        "USD"
      ],
      [
        469.0882278588,
        20240310,
        "Virtual Machines",
        "USD"
      ],
      [
        2.44850851754565,
        20240310,
        "Virtual Network",
        "USD"
      ],
      [
        5.1,
        20240310,
        "Virtual WAN",
        "USD"
      ],
      [
        19.7580482890772,
        20240311,
        "Application Gateway",
        "USD"
      ],
      [
        0.0276094148387097,
        20240311,
        "Azure DNS",
        "USD"
      ],
      [
        20.0550361215968,
        20240311,
        "Azure Database for MySQL",
        "USD"
      ],
      [
        17.3675571334158,
        20240311,
        "Azure Front Door Service",
        "USD"
      ],
      [
        86.4257911063407,
        20240311,
        "Bandwidth",
        "USD"
      ],
      [
        0.000006308233216,
        20240311,
        "Content Delivery Network",
        "USD"
      ],
      [
        0.00080835,
        20240311,
        "Key Vault",
        "USD"
      ],
      [
        0.511200022422755,
        20240311,
        "Load Balancer",
        "USD"
      ],
      [
        0,
        20240311,
        "Log Analytics",
        "USD"
      ],
      [
        1.00813748500915,
        20240311,
        "NAT Gateway",
        "USD"
      ],
      [
        200.208505820224,
        20240311,
        "Storage",
        "USD"
      ],
      [
        0.00987096774193551,
        20240311,
        "Traffic Manager",
        "USD"
      ],
      [
        0,
        20240311,
        "Unassigned",
        "USD"
      ],
      [
        11.5056,
        20240311,
        "VPN Gateway",
        "USD"
      ],
      [
        438.2589280007,
        20240311,
        "Virtual Machines",
        "USD"
      ],
      [
        2.51948184889706,
        20240311,
        "Virtual Network",
        "USD"
      ],
      [
        5.1,
        20240311,
        "Virtual WAN",
        "USD"
      ],
      [
        25.3376944369115,
        20240312,
        "Application Gateway",
        "USD"
      ],
      [
        0.0275726948387097,
        20240312,
        "Azure DNS",
        "USD"
      ],
      [
        0.000017,
        20240312,
        "Azure Data Factory v2",
        "USD"
      ],
      [
        20.0633006820968,
        20240312,
        "Azure Database for MySQL",
        "USD"
      ],
      [
        18.0454466787521,
        20240312,
        "Azure Front Door Service",
        "USD"
      ],
      [
        148.425003358589,
        20240312,
        "Bandwidth",
        "USD"
      ],
      [
        0.0000115213571457024,
        20240312,
        "Content Delivery Network",
        "USD"
      ],
      [
        0.0008058,
        20240312,
        "Key Vault",
        "USD"
      ],
      [
        0.51120000313879,
        20240312,
        "Load Balancer",
        "USD"
      ],
      [
        0,
        20240312,
        "Log Analytics",
        "USD"
      ],
      [
        0.982056408765726,
        20240312,
        "NAT Gateway",
        "USD"
      ],
      [
        200.7293277066,
        20240312,
        "Storage",
        "USD"
      ],
      [
        0.0193218312096775,
        20240312,
        "Traffic Manager",
        "USD"
      ],
      [
        0,
        20240312,
        "Unassigned",
        "USD"
      ],
      [
        11.5056,
        20240312,
        "VPN Gateway",
        "USD"
      ],
      [
        413.842249647,
        20240312,
        "Virtual Machines",
        "USD"
      ],
      [
        2.6725198794409,
        20240312,
        "Virtual Network",
        "USD"
      ],
      [
        5.1,
        20240312,
        "Virtual WAN",
        "USD"
      ],
      [
        28.3951922033898,
        20240313,
        "Application Gateway",
        "USD"
      ],
      [
        0.0275920748387097,
        20240313,
        "Azure DNS",
        "USD"
      ],
      [
        0.000017,
        20240313,
        "Azure Data Factory v2",
        "USD"
      ],
      [
        20.0565085170968,
        20240313,
        "Azure Database for MySQL",
        "USD"
      ],
      [
        17.8694271510809,
        20240313,
        "Azure Front Door Service",
        "USD"
      ],
      [
        153.603305138117,
        20240313,
        "Bandwidth",
        "USD"
      ],
      [
        0.000765,
        20240313,
        "Key Vault",
        "USD"
      ],
      [
        0.511200008122064,
        20240313,
        "Load Balancer",
        "USD"
      ],
      [
        0,
        20240313,
        "Log Analytics",
        "USD"
      ],
      [
        1.01158896337543,
        20240313,
        "NAT Gateway",
        "USD"
      ],
      [
        200.6642118538,
        20240313,
        "Storage",
        "USD"
      ],
      [
        0.0246774193548388,
        20240313,
        "Traffic Manager",
        "USD"
      ],
      [
        0,
        20240313,
        "Unassigned",
        "USD"
      ],
      [
        11.5056,
        20240313,
        "VPN Gateway",
        "USD"
      ],
      [
        413.8289203941,
        20240313,
        "Virtual Machines",
        "USD"
      ],
      [
        2.75641892109998,
        20240313,
        "Virtual Network",
        "USD"
      ],
      [
        5.1,
        20240313,
        "Virtual WAN",
        "USD"
      ],
      [
        28.6018043566384,
        20240314,
        "Application Gateway",
        "USD"
      ],
      [
        0.0276073748387097,
        20240314,
        "Azure DNS",
        "USD"
      ],
      [
        0.000017,
        20240314,
        "Azure Data Factory v2",
        "USD"
      ],
      [
        20.0514698550968,
        20240314,
        "Azure Database for MySQL",
        "USD"
      ],
      [
        17.0457381418108,
        20240314,
        "Azure Front Door Service",
        "USD"
      ],
      [
        152.455979992844,
        20240314,
        "Bandwidth",
        "USD"
      ],
      [
        0.0006936,
        20240314,
        "Key Vault",
        "USD"
      ],
      [
        0.51120009274669,
        20240314,
        "Load Balancer",
        "USD"
      ],
      [
        0,
        20240314,
        "Log Analytics",
        "USD"
      ],
      [
        0.9879153954098,
        20240314,
        "NAT Gateway",
        "USD"
      ],
      [
        200.6692124114,
        20240314,
        "Storage",
        "USD"
      ],
      [
        0.0246774193548388,
        20240314,
        "Traffic Manager",
        "USD"
      ],
      [
        0,
        20240314,
        "Unassigned",
        "USD"
      ],
      [
        11.5056,
        20240314,
        "VPN Gateway",
        "USD"
      ],
      [
        409.2308057176,
        20240314,
        "Virtual Machines",
        "USD"
      ],
      [
        2.75524949281896,
        20240314,
        "Virtual Network",
        "USD"
      ],
      [
        5.1,
        20240314,
        "Virtual WAN",
        "USD"
      ],
      [
        23.5813299087035,
        20240315,
        "Application Gateway",
        "USD"
      ],
      [
        0.0276539548387097,
        20240315,
        "Azure DNS",
        "USD"
      ],
      [
        0.000017,
        20240315,
        "Azure Data Factory v2",
        "USD"
      ],
      [
        20.0472061380968,
        20240315,
        "Azure Database for MySQL",
        "USD"
      ],
      [
        16.4459005376344,
        20240315,
        "Azure Front Door Service",
        "USD"
      ],
      [
        138.643670269111,
        20240315,
        "Bandwidth",
        "USD"
      ],
      [
        0.0006477,
        20240315,
        "Key Vault",
        "USD"
      ],
      [
        0.511200341229606,
        20240315,
        "Load Balancer",
        "USD"
      ],
      [
        0,
        20240315,
        "Log Analytics",
        "USD"
      ],
      [
        1.03968370248587,
        20240315,
        "NAT Gateway",
        "USD"
      ],
      [
        200.7206199882,
        20240315,
        "Storage",
        "USD"
      ],
      [
        0.0246774193548388,
        20240315,
        "Traffic Manager",
        "USD"
      ],
      [
        0,
        20240315,
        "Unassigned",
        "USD"
      ],
      [
        11.5056,
        20240315,
        "VPN Gateway",
        "USD"
      ],
      [
        413.8197312501,
        20240315,
        "Virtual Machines",
        "USD"
      ],
      [
        2.76153234035382,
        20240315,
        "Virtual Network",
        "USD"
      ],
      [
        5.1,
        20240315,
        "Virtual WAN",
        "USD"
      ],
      [
        22.9722541525424,
        20240316,
        "Application Gateway",
        "USD"
      ],
      [
        0.0276546348387097,
        20240316,
        "Azure DNS",
        "USD"
      ],
      [
        20.0447870940968,
        20240316,
        "Azure Database for MySQL",
        "USD"
      ],
      [
        16.3262300437571,
        20240316,
        "Azure Front Door Service",
        "USD"
      ],
      [
        141.86074628915,
        20240316,
        "Bandwidth",
        "USD"
      ],
      [
        0.0006426,
        20240316,
        "Key Vault",
        "USD"
      ],
      [
        0.511200003118999,
        20240316,
        "Load Balancer",
        "USD"
      ],
      [
        0,
        20240316,
        "Log Analytics",
        "USD"
      ],
      [
        1.27902469958807,
        20240316,
        "NAT Gateway",
        "USD"
      ],
      [
        200.6705056675,
        20240316,
        "Storage",
        "USD"
      ],
      [
        0.0246774193548388,
        20240316,
        "Traffic Manager",
        "USD"
      ],
      [
        0,
        20240316,
        "Unassigned",
        "USD"
      ],
      [
        11.5056,
        20240316,
        "VPN Gateway",
        "USD"
      ],
      [
        413.8522278588,
        20240316,
        "Virtual Machines",
        "USD"
      ],
      [
        2.75498056321545,
        20240316,
        "Virtual Network",
        "USD"
      ],
      [
        5.1,
        20240316,
        "Virtual WAN",
        "USD"
      ],
      [
        22.9711851694915,
        20240317,
        "Application Gateway",
        "USD"
      ],
      [
        0.0276607548387097,
        20240317,
        "Azure DNS",
        "USD"
      ],
      [
        0.000017,
        20240317,
        "Azure Data Factory v2",
        "USD"
      ],
      [
        20.0417389770968,
        20240317,
        "Azure Database for MySQL",
        "USD"
      ],
      [
        15.2748655913979,
        20240317,
        "Azure Front Door Service",
        "USD"
      ],
      [
        143.915453329647,
        20240317,
        "Bandwidth",
        "USD"
      ],
      [
        0.0006426,
        20240317,
        "Key Vault",
        "USD"
      ],
      [
        0.511200001820736,
        20240317,
        "Load Balancer",
        "USD"
      ],
      [
        0,
        20240317,
        "Log Analytics",
        "USD"
      ],
      [
        1.32165927948011,
        20240317,
        "NAT Gateway",
        "USD"
      ],
      [
        200.6700705229,
        20240317,
        "Storage",
        "USD"
      ],
      [
        0.0246774193548388,
        20240317,
        "Traffic Manager",
        "USD"
      ],
      [
        0,
        20240317,
        "Unassigned",
        "USD"
      ],
      [
        11.5056,
        20240317,
        "VPN Gateway",
        "USD"
      ],
      [
        413.8555539294,
        20240317,
        "Virtual Machines",
        "USD"
      ],
      [
        2.75490995341726,
        20240317,
        "Virtual Network",
        "USD"
      ],
      [
        5.1,
        20240317,
        "Virtual WAN",
        "USD"
      ],
      [
        22.9678255084746,
        20240318,
        "Application Gateway",
        "USD"
      ],
      [
        0.0275743948387097,
        20240318,
        "Azure DNS",
        "USD"
      ],
      [
        0.000017,
        20240318,
        "Azure Data Factory v2",
        "USD"
      ],
      [
        20.0621321865968,
        20240318,
        "Azure Database for MySQL",
        "USD"
      ],
      [
        16.3263066682598,
        20240318,
        "Azure Front Door Service",
        "USD"
      ],
      [
        153.538162828273,
        20240318,
        "Bandwidth",
        "USD"
      ],
      [
        0.0006426,
        20240318,
        "Key Vault",
        "USD"
      ],
      [
        0.511296227722708,
        20240318,
        "Load Balancer",
        "USD"
      ],
      [
        0,
        20240318,
        "Log Analytics",
        "USD"
      ],
      [
        1.36739995743264,
        20240318,
        "NAT Gateway",
        "USD"
      ],
      [
        200.7017396082,
        20240318,
        "Storage",
        "USD"
      ],
      [
        0.0246774193548388,
        20240318,
        "Traffic Manager",
        "USD"
      ],
      [
        0,
        20240318,
        "Unassigned",
        "USD"
      ],
      [
        11.5056,
        20240318,
        "VPN Gateway",
        "USD"
      ],
      [
        413.8555539294,
        20240318,
        "Virtual Machines",
        "USD"
      ],
      [
        2.75997228129348,
        20240318,
        "Virtual Network",
        "USD"
      ],
      [
        5.1,
        20240318,
        "Virtual WAN",
        "USD"
      ],
      [
        22.9674246398305,
        20240319,
        "Application Gateway",
        "USD"
      ],
      [
        0.0277460948387097,
        20240319,
        "Azure DNS",
        "USD"
      ],
      [
        0.000017,
        20240319,
        "Azure Data Factory v2",
        "USD"
      ],
      [
        20.0545711545968,
        20240319,
        "Azure Database for MySQL",
        "USD"
      ],
      [
        15.5319297544322,
        20240319,
        "Azure Front Door Service",
        "USD"
      ],
      [
        176.066783562374,
        20240319,
        "Bandwidth",
        "USD"
      ],
      [
        0.0006426,
        20240319,
        "Key Vault",
        "USD"
      ],
      [
        0.511200227568206,
        20240319,
        "Load Balancer",
        "USD"
      ],
      [
        0,
        20240319,
        "Log Analytics",
        "USD"
      ],
      [
        1.39275404470414,
        20240319,
        "NAT Gateway",
        "USD"
      ],
      [
        200.6766160023,
        20240319,
        "Storage",
        "USD"
      ],
      [
        0.0246774193548388,
        20240319,
        "Traffic Manager",
        "USD"
      ],
      [
        0,
        20240319,
        "Unassigned",
        "USD"
      ],
      [
        11.5056,
        20240319,
        "VPN Gateway",
        "USD"
      ],
      [
        413.842249647,
        20240319,
        "Virtual Machines",
        "USD"
      ],
      [
        2.75603122274205,
        20240319,
        "Virtual Network",
        "USD"
      ],
      [
        5.1,
        20240319,
        "Virtual WAN",
        "USD"
      ],
      [
        22.9693717161017,
        20240320,
        "Application Gateway",
        "USD"
      ],
      [
        0.0278276948387097,
        20240320,
        "Azure DNS",
        "USD"
      ],
      [
        0.000017,
        20240320,
        "Azure Data Factory v2",
        "USD"
      ],
      [
        20.0616717780968,
        20240320,
        "Azure Database for MySQL",
        "USD"
      ],
      [
        16.1088991079731,
        20240320,
        "Azure Front Door Service",
        "USD"
      ],
      [
        174.206592774205,
        20240320,
        "Bandwidth",
        "USD"
      ],
      [
        0.00065025,
        20240320,
        "Key Vault",
        "USD"
      ],
      [
        0.511234507872071,
        20240320,
        "Load Balancer",
        "USD"
      ],
      [
        0,
        20240320,
        "Log Analytics",
        "USD"
      ],
      [
        1.36029259274667,
        20240320,
        "NAT Gateway",
        "USD"
      ],
      [
        200.6720553234,
        20240320,
        "Storage",
        "USD"
      ],
      [
        0.0246774193548388,
        20240320,
        "Traffic Manager",
        "USD"
      ],
      [
        0,
        20240320,
        "Unassigned",
        "USD"
      ],
      [
        11.5056,
        20240320,
        "VPN Gateway",
        "USD"
      ],
      [
        413.8555539294,
        20240320,
        "Virtual Machines",
        "USD"
      ],
      [
        2.75654775261693,
        20240320,
        "Virtual Network",
        "USD"
      ],
      [
        5.1,
        20240320,
        "Virtual WAN",
        "USD"
      ],
      [
        1.91756146186441,
        20240321,
        "Application Gateway",
        "USD"
      ],
      [
        0.00345699935483871,
        20240321,
        "Azure DNS",
        "USD"
      ],
      [
        0.835882604129032,
        20240321,
        "Azure Database for MySQL",
        "USD"
      ],
      [
        1.39381999980188,
        20240321,
        "Azure Front Door Service",
        "USD"
      ],
      [
        18.2779879397146,
        20240321,
        "Bandwidth",
        "USD"
      ],
      [
        0.000051,
        20240321,
        "Key Vault",
        "USD"
      ],
      [
        0.0639,
        20240321,
        "Load Balancer",
        "USD"
      ],
      [
        0,
        20240321,
        "Log Analytics",
        "USD"
      ],
      [
        0.109372382878326,
        20240321,
        "NAT Gateway",
        "USD"
      ],
      [
        24.1417830915,
        20240321,
        "Storage",
        "USD"
      ],
      [
        0.00308467741935485,
        20240321,
        "Traffic Manager",
        "USD"
      ],
      [
        0,
        20240321,
        "Unassigned",
        "USD"
      ],
      [
        0.9588,
        20240321,
        "VPN Gateway",
        "USD"
      ],
      [
        17.24412,
        20240321,
        "Virtual Machines",
        "USD"
      ],
      [
        0.344291560277808,
        20240321,
        "Virtual Network",
        "USD"
      ],
      [
        0.425,
        20240321,
        "Virtual WAN",
        "USD"
      ]
    ]
  }
}
```

