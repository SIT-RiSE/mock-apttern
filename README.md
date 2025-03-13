
# Mock Sequence Pattern Analyzer

## Overview
This tool categorizes and organizes mock patterns in Java test code using Mockito. It identifies and classifies mock sequences into 15 core patterns, providing a comprehensive overview of mock usage.

## Pattern Classification
### 1. Pattern Components
Each pattern is defined by **operation locations**:
```python
{
  "Create": ["Test Case", "Attribute", "@Before", "Helper Method"],
  "Stub":   ["Test Case", "None", "@Before", "Helper Method"],
  "Verify": ["Test Case", "None"]
}
```


## Usage
### Installation
```bash
pip install -r requirements.txt
```



## Output Structure

```
output/
├── project1/
│   ├── 1-Service-3/          # Pattern category directory
│   │   ├── 1-pattern1-5.json  # Individual pattern file
│   │   └── 2-pattern2-3.json
│   └── project1_summary.xlsx  # Project-level statistics
└── global_summary.xlsx        # Cross-project aggregation
```

### File/Directory Structure Explanation

1. **Project Directories** (e.g. `project1/`)
   - Contain analysis results for individual projects
   - Each has:
     - Pattern category directories
     - Project-level Excel summary

2. **Pattern Category Directories** (e.g. `1-Service-3/`)
   - Naming format: `[Rank]-[Type]-[Count]`
     - **Rank**: Pattern's frequency ranking
     - **Type**: Mock type classification (Service/Dao/Controller/etc)
     - **Count**: Number of cases in this category

3. **Pattern Files** (e.g. `1-pattern1-5.json`)
   - Naming format: `[ID]-[pattern]-[cases].json`
     - **ID**: Unique pattern identifier
     - **pattern**: Pattern name/number
     - **cases**: Number of mock sequences in this file
   - Contains detailed mock patterns:
     ```json
      {
        "variableName": "uuidMock",
        "variableType": "UUID",
        "mockedClass": "UUID",
        "isReuseableMock": false,
        "mockPattern": "Creation:\n— Attribute Mock Creation\n\nStubbing:\n— None\n\nVerification:\n— None",
        "classContext": {
          "packageName": "com.cloud.agent",
          "filePath": "C:\\java tool\\Apache\\cloudstack\\agent\\src\\test\\java\\com\\cloud\\agent\\AgentShellTest.java",
          "className": "AgentShellTest"
        },
        "statements": [
          {
            "type": "FIELD_MOCK_CREATION",
            "code": "@Mock\r\nUUID uuidMock;",
            "line": 58,
            "locate": "Attribute",
            "locationContext": {
              "methodName": "[FieldDeclaration]",
              "methodAnnotations": [
                "@Mock"
              ]
            }
          }
        ]
      }
     ```

4. **Excel Reports**
   - `project1_summary.xlsx` (Per-project)
     - Columns:
       | Column | Description |
       |---|---|
       | Dependency | Mocked component type |
       | Total | Total mocks per type |
       | Pattern1-Pattern15 | Frequency of predefined patterns |
       | Other | Unclassified patterns |

   - `global_summary.xlsx` (Cross-project)
     - Columns:
       | Column | Description |
       |---|---|
       | Project | Project name |
       | Total | Total mocks in project |
       | Pattern1-Pattern15 | Pattern distribution |
       | Other | Unclassified patterns |

### JSON Structure Key Fields
- **variableName**: Name of mock variable in test
- **mockedClass**: Original class being mocked
- **mockPattern**: Pattern classification with:
  - Creation method
  - Stubbing techniques
  - Verification approaches
- **pattern_id**: Unique pattern identifier (1-15)
- **statements**: Detailed code interactions
- **classContext**: Source code location metadata

This structure enables:
1. Quick pattern frequency analysis via Excel
2. Deep pattern inspection through JSON files
3. Cross-project comparisons using global summary
4. Pattern evolution tracking through versioned outputs

## Why 15 Patterns?
We focus on these 15 patterns because:
- They cover **97%** of 11,334 analyzed mock objects
- The remaining 58 patterns account for just **2%** combined

