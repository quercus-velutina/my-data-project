Fortellis Routing

{
  "name": "CDK | Fortellis | Logging | Fortellis_Routing (Modern APIs)",
  "description": null,
  "permissions": "PUBLIC_READ_WRITE",
  "pages": [
    {
      "guid": "MzM1NjQ4N3xWSVp8REFTSEJPQVJEfDExOTk0Nzkx",
      "name": "CDK | Fortellis | Logging | Smart Hulk APIs",
      "description": null,
      "widgets": [
        {
          "id": "244807562",
          "title": "",
          "layout": {
            "column": 1,
            "row": 1,
            "width": 12,
            "height": 1
          },
          "linkedEntityGuids": null,
          "visualization": {
            "id": "viz.billboard"
          },
          "rawConfiguration": {
            "facet": {
              "showOtherSeries": false
            },
            "nrqlQueries": [
              {
                "accountIds": [
                  3356487
                ],
                "query": "SELECT count(*) as 'Total #Requests', average(metrics.total_duration_ms) as 'Total Average Duration(in ms)', average(metrics.provider.provider_duration_ms) as 'Average Time spent in Provider(in ms)', average(metrics.proxy.proxy_duration_ms) as 'Average Time spent in APIGEE(in ms)', average(responseTime) as 'ResponseTime(in ms)' FROM Log WHERE (context = 'FORTELLIS_ROUTING' AND apigee.apigeeEnv = 'prod') OR (context LIKE 'CDK_DRIVE%')"
              }
            ],
            "platformOptions": {
              "ignoreTimeRange": false
            }
          }
        },
        {
          "id": "447790839",
          "title": "all logs",
          "layout": {
            "column": 1,
            "row": 2,
            "width": 12,
            "height": 4
          },
          "linkedEntityGuids": [],
          "visualization": {
            "id": "logger.log-table-widget"
          },
          "rawConfiguration": {
            "nrqlQueries": [
              {
                "accountIds": [
                  3356487
                ],
                "query": "FROM Log SELECT context, appName, `response.code`, `provider.name`, httpMethod, subscriptionOrgName, subscriptionOrgId, `subscriptionId`, clientRequestId, fortRequestId, longOpId, subscriptionOrgId, proxyBasepath, httpRoute, longOpRoute, `queryString`, `response.message`, faultSource, errorContent.message, metrics.total_duration_ms, metrics.provider.provider_duration_ms LIMIT MAX"
              }
            ]
          }
        },
        {
          "id": "446637713",
          "title": "all logs",
          "layout": {
            "column": 1,
            "row": 6,
            "width": 12,
            "height": 4
          },
          "linkedEntityGuids": [
            "MzM1NjQ4N3xWSVp8REFTSEJPQVJEfDExOTk0Nzkx"
          ],
          "visualization": {
            "id": "viz.bar"
          },
          "rawConfiguration": {
            "facet": {
              "showOtherSeries": false
            },
            "nrqlQueries": [
              {
                "accountIds": [
                  3356487
                ],
                "query": "FROM Log SELECT count(*) FACET context LIMIT 20"
              }
            ],
            "platformOptions": {
              "ignoreTimeRange": false
            }
          }
        },
        {
          "id": "307929378",
          "title": "",
          "layout": {
            "column": 1,
            "row": 10,
            "width": 3,
            "height": 3
          },
          "linkedEntityGuids": [
            "MzM1NjQ4N3xWSVp8REFTSEJPQVJEfDExOTk0Nzkx"
          ],
          "visualization": {
            "id": "viz.pie"
          },
          "rawConfiguration": {
            "colors": {
              "seriesOverrides": [
                {
                  "color": "#07b61b",
                  "seriesName": "Successful"
                },
                {
                  "color": "#af2c2c",
                  "seriesName": "Failed"
                }
              ]
            },
            "facet": {
              "showOtherSeries": true
            },
            "legend": {
              "enabled": true
            },
            "nrqlQueries": [
              {
                "accountIds": [
                  3356487
                ],
                "query": "SELECT count(*) as 'Requests' FROM Log WHERE context = 'FORTELLIS_ROUTING' AND apigee.apigeeEnv = 'prod' AND apiEnv = 'prod' FACET CASES(where isErrorResponse = true as 'Failed', where isErrorResponse = false as 'Successful') SINCE 1 day ago UNTIL now"
              }
            ],
            "platformOptions": {
              "ignoreTimeRange": false
            }
          }
        },
        {
          "id": "233706379",
          "title": "Fault Source",
          "layout": {
            "column": 4,
            "row": 10,
            "width": 4,
            "height": 3
          },
          "linkedEntityGuids": null,
          "visualization": {
            "id": "viz.pie"
          },
          "rawConfiguration": {
            "colors": {
              "seriesOverrides": [
                {
                  "color": "#8f09d7",
                  "seriesName": "Fortellis"
                },
                {
                  "color": "#1669d4",
                  "seriesName": "N/A"
                }
              ]
            },
            "facet": {
              "showOtherSeries": true
            },
            "legend": {
              "enabled": true
            },
            "nrqlQueries": [
              {
                "accountIds": [
                  3356487
                ],
                "query": "SELECT count(*) FROM Log WHERE context = 'FORTELLIS_ROUTING' AND apigee.apigeeEnv = 'prod' AND apiEnv = 'prod' FACET faultSource SINCE 1 day ago UNTIL now"
              }
            ],
            "platformOptions": {
              "ignoreTimeRange": false
            }
          }
        },
        {
          "id": "455977317",
          "title": "response.code by provider and app",
          "layout": {
            "column": 8,
            "row": 10,
            "width": 5,
            "height": 3
          },
          "linkedEntityGuids": null,
          "visualization": {
            "id": "viz.line"
          },
          "rawConfiguration": {
            "colors": {
              "seriesOverrides": [
                {
                  "color": "#1fd643",
                  "seriesName": "200"
                },
                {
                  "color": "#89f09e",
                  "seriesName": "202"
                },
                {
                  "color": "#4f873b",
                  "seriesName": "201"
                }
              ]
            },
            "facet": {
              "showOtherSeries": false
            },
            "legend": {
              "enabled": true
            },
            "markers": {
              "displayedTypes": {
                "criticalViolations": false,
                "deployments": true,
                "relatedDeployments": true,
                "warningViolations": false
              }
            },
            "nrqlQueries": [
              {
                "accountIds": [
                  3356487
                ],
                "query": "FROM Log SELECT count(*) FACET response.code WHERE apigee.apigeeEnv = 'prod' AND appName NOT LIKE '%Test%' LIMIT MAX TIMESERIES AUTO"
              }
            ],
            "platformOptions": {
              "ignoreTimeRange": false
            },
            "thresholds": {
              "isLabelVisible": true
            },
            "yAxisLeft": {
              "zero": true
            },
            "yAxisRight": {
              "zero": true
            }
          }
        },
        {
          "id": "176178778",
          "title": "response.code by provider and app",
          "layout": {
            "column": 8,
            "row": 13,
            "width": 5,
            "height": 3
          },
          "linkedEntityGuids": [],
          "visualization": {
            "id": "viz.pie"
          },
          "rawConfiguration": {
            "facet": {
              "showOtherSeries": true
            },
            "legend": {
              "enabled": true
            },
            "nrqlQueries": [
              {
                "accountIds": [
                  3356487
                ],
                "query": "FROM Log SELECT count(*) FACET response.code WHERE apigee.apigeeEnv = 'prod' AND appName NOT LIKE '%Test%' LIMIT MAX"
              }
            ],
            "platformOptions": {
              "ignoreTimeRange": false
            }
          }
        },
        {
          "id": "438461888",
          "title": "response.code by provider and app",
          "layout": {
            "column": 1,
            "row": 16,
            "width": 10,
            "height": 2
          },
          "linkedEntityGuids": null,
          "visualization": {
            "id": "viz.table"
          },
          "rawConfiguration": {
            "facet": {
              "showOtherSeries": false
            },
            "nrqlQueries": [
              {
                "accountIds": [
                  3356487
                ],
                "query": "FROM Log SELECT count(*) FACET appName, proxyBasepath, httpRoute, response.code LIMIT 10"
              }
            ],
            "platformOptions": {
              "ignoreTimeRange": false
            }
          }
        },
        {
          "id": "246448220",
          "title": "response.code by provider and app",
          "layout": {
            "column": 1,
            "row": 18,
            "width": 10,
            "height": 2
          },
          "linkedEntityGuids": [],
          "visualization": {
            "id": "viz.table"
          },
          "rawConfiguration": {
            "facet": {
              "showOtherSeries": false
            },
            "nrqlQueries": [
              {
                "accountIds": [
                  3356487
                ],
                "query": "FROM Log SELECT count(*) FACET appName, subscriptionOrgName, subscriptionId, response.code LIMIT 10"
              }
            ],
            "platformOptions": {
              "ignoreTimeRange": false
            }
          }
        },
        {
          "id": "438477429",
          "title": "response.code by provider and app",
          "layout": {
            "column": 1,
            "row": 20,
            "width": 10,
            "height": 2
          },
          "linkedEntityGuids": null,
          "visualization": {
            "id": "viz.table"
          },
          "rawConfiguration": {
            "facet": {
              "showOtherSeries": false
            },
            "nrqlQueries": [
              {
                "accountIds": [
                  3356487
                ],
                "query": "FROM Log SELECT count(*) FACET appName, subscriptionOrgName, subscriptionId, response.code LIMIT 10"
              }
            ],
            "platformOptions": {
              "ignoreTimeRange": false
            }
          }
        },
        {
          "id": "251712653",
          "title": "Accept-Encoding",
          "layout": {
            "column": 1,
            "row": 22,
            "width": 4,
            "height": 3
          },
          "linkedEntityGuids": null,
          "visualization": {
            "id": "viz.line"
          },
          "rawConfiguration": {
            "facet": {
              "showOtherSeries": false
            },
            "legend": {
              "enabled": true
            },
            "markers": {
              "displayedTypes": {
                "criticalViolations": false,
                "deployments": true,
                "relatedDeployments": true,
                "warningViolations": false
              }
            },
            "nrqlQueries": [
              {
                "accountIds": [
                  3356487
                ],
                "query": "FROM Log SELECT count(*) FACET `responseHeaders.content-encoding` WHERE provider.name != 'dms-accounting-payables-pending-invoices API' SINCE 3 days ago TIMESERIES"
              }
            ],
            "platformOptions": {
              "ignoreTimeRange": false
            },
            "thresholds": {
              "isLabelVisible": true
            },
            "yAxisLeft": {
              "zero": true
            },
            "yAxisRight": {
              "zero": true
            }
          }
        },
        {
          "id": "445439397",
          "title": "Uniques(response.code) by SubID",
          "layout": {
            "column": 5,
            "row": 22,
            "width": 6,
            "height": 3
          },
          "linkedEntityGuids": null,
          "visualization": {
            "id": "viz.table"
          },
          "rawConfiguration": {
            "facet": {
              "showOtherSeries": false
            },
            "nrqlQueries": [
              {
                "accountIds": [
                  3356487
                ],
                "query": "FROM Log SELECT uniques(subscriptionId), uniques(response.code) WHERE context IN ('FORTELLIS_ROUTING','FORTELLIS_EVENT_RELAY') AND response.code > 399 AND response.code IS NOT NULL LIMIT 100 "
              }
            ],
            "platformOptions": {
              "ignoreTimeRange": false
            }
          }
        },
        {
          "id": "176178780",
          "title": "Uniques(response.code) by SubID",
          "layout": {
            "column": 5,
            "row": 25,
            "width": 6,
            "height": 3
          },
          "linkedEntityGuids": [],
          "visualization": {
            "id": "viz.line"
          },
          "rawConfiguration": {
            "facet": {
              "showOtherSeries": false
            },
            "legend": {
              "enabled": true
            },
            "markers": {
              "displayedTypes": {
                "criticalViolations": false,
                "deployments": true,
                "relatedDeployments": true,
                "warningViolations": false
              }
            },
            "nrqlQueries": [
              {
                "accountIds": [
                  3356487
                ],
                "query": "FROM Log SELECT count(*) FACET response.code, subscriptionId WHERE (subscriptionId IN ('8a071770-59c9-4f40-9b71-fd1ed35b6663','eb964d73-f0ec-4b5d-8f2e-7ca8aae1da3d','ffd326fb-c218-4005-89d7-772f4888e203','99bd0790-ca6c-444d-9cb4-54b26fb9ff80','36802a9d-e7cf-4f6e-a6c6-7af6209c84eb','3e86c4a6-45c9-440f-a014-f842fa7a7c3b','5da1c3a5-1e74-4c4e-87ed-bcdc6c3e3ce5','8051a248-3b65-4bdc-89df-88dfa30191b2','68e81f9a-ee95-49b5-aa07-a3ac1669b90b','3a32a342-2dde-4a17-8b5d-380af082c675','c14fb941-c326-4051-8b8c-73a7a2ea1cb7','72c2b1c8-51a4-4a6f-8bba-b4b08ccf68d2','5000e36e-1bb3-4a05-a176-bf16bed691a5','30e65745-ae7b-47c0-bef6-3d67f9f2aeac','a5462f9d-cfb1-4803-adce-86e328d80333','b0c24698-1f02-4deb-8fe0-bf7c63cac3bb','5170a8aa-5e62-4dc5-8b1c-83048e711c78','a2b83fd9-0f25-4bbb-a179-d7dcb039e5b5') AND `response.code` > 499) TIMESERIES SINCE 3 days ago UNTIL now"
              }
            ],
            "platformOptions": {
              "ignoreTimeRange": false
            },
            "thresholds": {
              "isLabelVisible": true
            },
            "yAxisLeft": {
              "zero": true
            },
            "yAxisRight": {
              "zero": true
            }
          }
        }
      ]
    }
  ],
  "variables": []
}