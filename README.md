
# L.E.A.P

Law Enforcement Automated Promotions

LEAP is a FiveM resource for FivePD that allows server owners to automate promotions based on a number of submitted arrest reports, callout reports and pedestrian citations.

#### This __ONLY__ works if you are using **MySQL for fivepd**. I may change it to support SQLite in the future, but don't hold your breath. Please do not ask/spam on Discord.
## Installation

Installation is like any other FiveM resource. Extract the folder into your resources folder.
## Configuration
### Client
LEAP, on the client side, will query for a promotion every 15 minutes. This delay **IS** configurable by way of a [Convar](https://docs.fivem.net/docs/scripting-reference/convars/) - Simply add `set LEAPAutoRankDelay 15000` to your server.cfg! **The integer value is in milliseconds**, and I do not recommend that you make it anything less than 15000 (15 minutes).

--- 
### Server
LEAP's configuration is driven by a "server-config.json" file located inside of 'LEAP/server'.

Below is a short guide explaining the purpose of each section of the server-config.json file:


**'fivepdResourceName'**: Should be left as is unless, for some reason, your fivepd folder inside of your resource folder is called something else
```JSON
"fivepdResourceName": "fivepd",
```
**'database'**: This should match your database configuration inside of your fivepd config
```JSON
"database": {
    "username": "root",
    "password": "root",
    "host": "MySQL",
    "port": 3306
    "database": "fivepd",
}
```
**'autoRanker'**: Here is where you configure multiple things, including minimum character length of reports, a date to check for reports from, and all of your departments, department ranks, the criteria for each rank, and a blacklist of player licenses

**minimumReportCharacterLimit**: The minimum number of characters that must be present in a player's report(s) to be considered eligible for a promotion check.

**effectiveFromDate**: A date from which all reports will be examined. Any reports BEFORE this date are excluded in the promotion check. This value must be a string and must be formatted as MM/DD/YYYY, e.g. `"04/24/2024"` (April 24th 2024) -- **If you do not know what you are doing, please leave this value as is**.

**departments**: Departments is an array. Inside of it, you will define the following:, 
- name: **Must match the name of the department in the CAD/MDT/Database**

- id: **Must match the name of the department in the CAD/MDT/Database**

- **ranks**: Like departments, this is another array, inside of it you will define the following:
    - name: **Must match the name of the rank in the CAD/MDT/Database**
    - prerequisites: Like departments and ranks, this is yet another array. Inside of it you will define the number of arrest reports, default reports, and ped citations that a player must have in order to be promoted to that rank
**blacklist**: A string array where you can put a player's license identifier to exclude them from automatic promotions. Self explanatory, really.

For your assistance:
- arrestReports: The report generated when you click "New Arrest"
- defaultReports: The report you fill out after a callout
- pedCitations: A citation/ticket issued to a ped when you search their name in the CAD/MDT
```JSON
  "autoRanker": {
    "minimumReportCharacterLimit": 50,
    "effectiveFromDate": "",
    "departments": [
      {
        "name": "LSPD",
        "id": 1,
        "ranks": [
          {
            "name": "Cadet",
            "prerequisites": {
              "arrestReports": 0,
              "defaultReports": 0,
              "pedCitations": 0
            }
          },
          {
            "name": "Officer I",
            "prerequisites": {
              "arrestReports": 10,
              "defaultReports": 10,
              "pedCitations": 10
            }
          },
          {
            "name": "Officer II",
            "prerequisites": {
              "arrestReports": 20,
              "defaultReports": 20,
              "pedCitations": 20
            }
          },
          {
            "name": "Officer III",
            "prerequisites": {
              "arrestReports": 30,
              "defaultReports": 30,
              "pedCitations": 30
            }
          },
          {
            "name": "Detective I",
            "prerequisites": {
              "arrestReports": 40,
              "defaultReports": 40,
              "pedCitations": 40
            }
          },
          {
            "name": "Detective II",
            "prerequisites": {
              "arrestReports": 50,
              "defaultReports": 50,
              "pedCitations": 50
            }
          },
          {
            "name": "Sergeant I",
            "prerequisites": {
              "arrestReports": 60,
              "defaultReports": 60,
              "pedCitations": 60
            }
          },
          {
            "name": "Sergeant II",
            "prerequisites": {
              "arrestReports": 70,
              "defaultReports": 70,
              "pedCitations": 70
            }
          },
          {
            "name": "Sergeant III",
            "prerequisites": {
              "arrestReports": 80,
              "defaultReports": 80,
              "pedCitations": 80
            }
          },
          {
            "name": "Lieutenant I",
            "prerequisites": {
              "arrestReports": 90,
              "defaultReports": 90,
              "pedCitations": 90
            }
          },
          {
            "name": "Lieutenant II",
            "prerequisites": {
              "arrestReports": 100,
              "defaultReports": 100,
              "pedCitations": 100
            }
          },
          {
            "name": "Lieutenant III",
            "prerequisites": {
              "arrestReports": 110,
              "defaultReports": 110,
              "pedCitations": 110
            }
          },
          {
            "name": "Captain",
            "prerequisites": {
              "arrestReports": 120,
              "defaultReports": 120,
              "pedCitations": 120
            }
          }
        ]
      }
    ],
    "blacklist": [
      "license1",
      "license2",
      "license3"
    ]
  }
  ```
## Example Configuration
```json
{
  "fivepdResourceName": "fivepd",
  "database": {
    "username": "root",
    "password": "root",
    "host": "MySQL",
    "port": 3306,
    "database": "fivepd"
  },
  "autoRanker": {
    "minimumReportCharacterLimit": 50,
    "effectiveFromDate": "",
    "departments": [
      {
        "name": "Los Santos Police Department",
        "id": 1,
        "ranks": [
          {
            "name": "Cadet",
            "prerequisites": {
              "arrestReports": 0,
              "defaultReports": 0,
              "pedCitations": 0
            }
          },
          {
            "name": "Officer I",
            "prerequisites": {
              "arrestReports": 10,
              "defaultReports": 10,
              "pedCitations": 10
            }
          },
          {
            "name": "Officer II",
            "prerequisites": {
              "arrestReports": 20,
              "defaultReports": 20,
              "pedCitations": 20
            }
          },
          {
            "name": "Officer III",
            "prerequisites": {
              "arrestReports": 30,
              "defaultReports": 30,
              "pedCitations": 30
            }
          },
          {
            "name": "Detective I",
            "prerequisites": {
              "arrestReports": 40,
              "defaultReports": 40,
              "pedCitations": 40
            }
          },
          {
            "name": "Detective II",
            "prerequisites": {
              "arrestReports": 50,
              "defaultReports": 50,
              "pedCitations": 50
            }
          },
          {
            "name": "Sergeant I",
            "prerequisites": {
              "arrestReports": 60,
              "defaultReports": 60,
              "pedCitations": 60
            }
          },
          {
            "name": "Sergeant II",
            "prerequisites": {
              "arrestReports": 70,
              "defaultReports": 70,
              "pedCitations": 70
            }
          },
          {
            "name": "Sergeant III",
            "prerequisites": {
              "arrestReports": 80,
              "defaultReports": 80,
              "pedCitations": 80
            }
          },
          {
            "name": "Lieutenant I",
            "prerequisites": {
              "arrestReports": 90,
              "defaultReports": 90,
              "pedCitations": 90
            }
          },
          {
            "name": "Lieutenant II",
            "prerequisites": {
              "arrestReports": 100,
              "defaultReports": 100,
              "pedCitations": 100
            }
          },
          {
            "name": "Lieutenant III",
            "prerequisites": {
              "arrestReports": 110,
              "defaultReports": 110,
              "pedCitations": 110
            }
          },
          {
            "name": "Captain",
            "prerequisites": {
              "arrestReports": 120,
              "defaultReports": 120,
              "pedCitations": 120
            }
          }
        ]
      }
    ],
    "blacklist": [
      "license1",
      "license2",
      "license3"
    ]
  }
}
```
