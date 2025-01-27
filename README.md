# Rwanda Locations JSON

A comprehensive JSON dataset containing Rwanda's administrative locations hierarchy, including Provinces, Districts, Sectors, Cells, and Villages.

## Description

This repository provides a structured JSON file containing the complete administrative divisions of Rwanda, from the highest level (Provinces) down to the lowest level (Villages). The data is organized hierarchically, making it easy to navigate through different administrative levels.

## Data Structure

The JSON structure follows Rwanda's administrative hierarchy:

```json
{
  "provinces": [
    {
      "name": "Province Name",
      "districts": [
        {
          "name": "District Name",
          "sectors": [
            {
              "name": "Sector Name",
              "cells": [
                {
                  "name": "Cell Name",
                  "villages": [
                    {
                      "name": "Village Name"
                    }
                  ]
                }
              ]
            }
          ]
        }
      ]
    }
  ]
}
```

## Installation

You can include this dataset in your project using several methods:

### Direct Download
Download the `locations.json` file directly from this repository and include it in your project.

### Using curl
```bash
curl -O https://raw.githubusercontent.com/jnkindi/rwanda-locations-json/master/locations.json
```

### Using wget
```bash
wget https://raw.githubusercontent.com/jnkindi/rwanda-locations-json/master/locations.json
```

## Usage

Here are some examples of how to use the data in different programming languages:

### JavaScript
```javascript
const locations = require('./locations.json');

// Get all provinces
const provinces = locations.provinces;

// Find a specific province
const kigaliCity = locations.provinces.find(province => 
  province.name.toLowerCase() === 'kigali city'
);

// Get districts of a province
const kigaliDistricts = kigaliCity.districts;

// Find a specific sector in a district
const findSector = (districtName, sectorName) => {
  const district = locations.provinces
    .flatMap(p => p.districts)
    .find(d => d.name.toLowerCase() === districtName.toLowerCase());
  
  return district?.sectors.find(s => 
    s.name.toLowerCase() === sectorName.toLowerCase()
  );
};
```

### Python
```python
import json

# Load the JSON file
with open('locations.json', 'r', encoding='utf-8') as file:
    locations = json.load(file)

# Get all provinces
provinces = locations['provinces']

# Find a specific district
def find_district(district_name):
    for province in locations['provinces']:
        for district in province['districts']:
            if district['name'].lower() == district_name.lower():
                return district
    return None

# Get all sectors in a district
def get_sectors(district_name):
    district = find_district(district_name)
    return district['sectors'] if district else []
```

## Data Coverage

The dataset includes:
- All 5 Provinces of Rwanda
- All 30 Districts
- All Sectors within each District
- All Cells within each Sector
- All Villages within each Cell

## Contributing

Contributions are welcome! If you find any inaccuracies or missing data, please:

1. Fork the repository
2. Create a new branch (`git checkout -b update-locations`)
3. Make your changes
4. Submit a Pull Request

Please ensure your updates include accurate source information for verification.

## Validation

To validate the JSON structure, you can use the following Node.js script:

```javascript
const fs = require('fs');

function validateLocations(filePath) {
  try {
    const data = JSON.parse(fs.readFileSync(filePath, 'utf8'));
    
    // Basic structure validation
    if (!Array.isArray(data.provinces)) {
      throw new Error('Provinces must be an array');
    }
    
    // Validate each level
    data.provinces.forEach((province, pIndex) => {
      if (!province.name || !Array.isArray(province.districts)) {
        throw new Error(`Invalid province at index ${pIndex}`);
      }
      
      province.districts.forEach((district, dIndex) => {
        if (!district.name || !Array.isArray(district.sectors)) {
          throw new Error(`Invalid district in province ${province.name}`);
        }
        // Add more validation as needed
      });
    });
    
    console.log('Validation successful!');
    return true;
  } catch (error) {
    console.error('Validation failed:', error.message);
    return false;
  }
}
```

## License

MIT License

## Credits

This dataset is maintained by the community and was initially created by [jnkindi](https://github.com/jnkindi).

## Support

If you encounter any issues or have questions, please:
1. Check existing issues in the repository
2. Create a new issue with a detailed description if your problem hasn't been reported
3. Include examples and context when reporting problems

## Updates

The dataset is periodically updated to reflect any administrative changes in Rwanda's locations. Check the repository's releases for the latest updates.

---
