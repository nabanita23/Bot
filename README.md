```
{
  "employmentStatus": {
    "retired": true,
    "student": false,
    "employed": false,
    "former": false,
    "selfEmployed": false,
    "unemployed": false,
    "other": false
  },
  "accountsWithOtherBanks": "Yes, Chase Bank & Citi Bank",
  "countryCitizenship": "United States Of America",
  "otherIncomeOtherPerson": [
    {
      "source": "Rental income",
      "amount": "12000"
    }
  ],
  "businessOwnership": [
    {
      "clientsNotableProducts": "Cleaning supplies, Disinfectants",
      "yearEstablished": "01/01/2015",
      "geographyOfMarkets": ["California", "Nevada"],
      "companyName": "Adam Supplies Inc.",
      "currentValueOfTheBusiness": "250000",
      "profitMargin": "15%",
      "numberOfLocations": "3",
      "natureOfBusiness": { "type": "Retail & Wholesale" },
      "estimatedAnnualNetIncome": "75000",
      "approximateInitialInvestment": "50000",
      "numberOfEmployees": "12"
    }
  ],
  "inheritanceGift": [
    {
      "generation": "Grandparent",
      "lastName": "Smith",
      "gender": "Male",
      "description": "Family estate",
      "estimatedAmountReceived": "100000",
      "suffix": "Jr.",
      "relationshipToGiftingParty": "Grandson",
      "otherLegalNames": "N/A",
      "estimatedPresentValue": "120000",
      "firstName": "John",
      "countryOfLastKnownResidence": "USA",
      "whenWasGiftOrInheritanceReceived": "2018-06-01",
      "additionalInvestmentRentalIncome": "5000",
      "middleName": "A",
      "natureOfTheAssetReceived": "Real Estate"
    }
  ],
  "sourceOfIncome": ["business", "investments"],
  "relationshipEstablished": "2017-03-15",
  "otherInstitutions": [
    {
      "institutionName": "Morgan Stanley"
    }
  ],
  "investmentsAppreciation": [
    {
      "descriptionOfTheInvestments": "Tech stocks portfolio",
      "estimatedInitialPurchaseSetupAmount": "15000",
      "describeRealEstate": "N/A",
      "describeAppreciation": "Increased 3x over 5 years",
      "additionalInvestmentRentalIncome": "0",
      "estimatedAmountOfSale": "45000",
      "approximateSalePrice": "50000",
      "yearTheBusinessWasSold": "2022",
      "assetType": {
        "physicalAsset": false,
        "investibleAsset": true
      }
    }
  ],
  "inheritanceGiftOtherPerson": [
    {
      "generation": "Parent",
      "lastName": "Johnson",
      "gender": "Female",
      "description": "Jewelry and Stocks",
      "estimatedAmountReceived": "30000",
      "suffix": "",
      "relationshipToGiftingParty": "Daughter",
      "otherLegalNames": "",
      "estimatedPresentValue": "35000",
      "firstName": "Emma",
      "countryOfLastKnownResidence": "USA",
      "whenWasGiftOrInheritanceReceived": "2020-12-10",
      "additionalInvestmentRentalIncome": "2000",
      "middleName": "L",
      "natureOfTheAssetReceived": "Jewelry & Stocks"
    }
  ],
  "employmentOtherPerson": [
    {
      "yearsOfService": "8",
      "nameOfEmployer": "Tesla Inc.",
      "approximateAnnualSalary": "120000",
      "positionsHeldAndTenure": "Engineer (5 years), Manager (3 years)",
      "descriptionOfTheBusiness": "Electric vehicles and energy"
    }
  ],
  "employment": [
    {
      "yearsOfService": "6",
      "nameOfEmployer": "Google LLC",
      "approximateAnnualSalary": "130000",
      "positionsHeldAndTenure": "Software Engineer (4 years), Tech Lead (2 years)",
      "descriptionOfTheBusiness": "Technology and Internet Services"
    }
  ],
  "saleOfAssetsBusiness": [
    {
      "estimatedInitialPurchaseSetupAmount": "40000",
      "describeRealEstate": "Office building in downtown LA",
      "yearSold": "2021",
      "companyName": "Legacy Holdings",
      "estimatedAmountOfSale": "150000",
      "countriesOfOperation": ["USA"],
      "approximateSalePrice": "170000"
    }
  ],
  "saleOfAssetsBusinessOtherPerson": [
    {
      "estimatedInitialPurchaseSetupAmount": "25000",
      "describeRealEstate": "Warehouse in Nevada",
      "yearSold": "2020",
      "companyName": "StorageMax",
      "estimatedAmountOfSale": "80000",
      "countriesOfOperation": ["USA"],
      "approximateSalePrice": "90000"
    }
  ],
  "businessOwnershipOtherPerson": [
    {
      "clientsNotableProducts": "Handcrafted goods",
      "yearEstablished": "2012",
      "geographyOfMarkets": ["Florida", "Texas"],
      "companyName": "CraftyHands Co.",
      "currentValueOfTheBusiness": "100000",
      "yearEstablished1": "2012",
      "profitMargin": "20%",
      "numberOfLocations": "2",
      "natureOfBusiness": { "type": "E-commerce" },
      "estimatedAnnualNetIncome": "30000",
      "approximateInitialInvestment": "15000",
      "numberOfEmployees": "5"
    }
  ],
  "investmentsAppreciationOtherPerson": [
    {
      "descriptionOfTheInvestments": "Mutual funds",
      "estimatedInitialPurchaseSetupAmount": "10000",
      "describeRealEstate": "",
      "describeAppreciation": "Grew 2x over 4 years",
      "additionalInvestmentRentalIncome": "0",
      "estimatedAmountOfSale": "20000",
      "approximateSalePrice": "22000",
      "yearTheBusinessWasSold": "2023",
      "assetType": {
        "physicalAsset": false,
        "investibleAsset": true
      }
    }
  ]
}

```
```
function getSelectedLabels(schema, selectedValues) {
  if (!schema?.data?.values || !Array.isArray(selectedValues)) {
    return [];
  }

  const valueToLabelMap = schema.data.values.reduce((map, item) => {
    map[item.value] = item.label;
    return map;
  }, {});

  return selectedValues.map(value => valueToLabelMap[value]).filter(Boolean);
}

```


const fs = require("fs").promises;

/**
 * Build a key-value map from flat form data to resolve conditional dependencies.
 */
const extractFieldValues = (formSections) => {
  const values = {};
  for (const { data } of formSections) {
    for (const field of data) {
      if (field?.key && field.value !== undefined) {
        values[field.key] = field.value;
      }
    }
  }
  return values;
};

/**
 * Evaluate if a field passes its conditional logic.
 */
const isFieldVisible = (field, valuesMap) => {
  const cond = field.conditional;
  if (!cond) return true;

  const actual = valuesMap[cond.when];

  if (cond.show === true) return actual === cond.eq;
  if (cond.show === false) return actual !== cond.eq;

  return true;
};

/**
 * Removes fields from form sections based on failed conditional logic.
 */
const cleanConditionalFields = (formSections) => {
  const valuesMap = extractFieldValues(formSections);

  return formSections.map(({ title, data }) => ({
    title,
    data: data.filter((field) => isFieldVisible(field, valuesMap)),
  }));
};

/**
 * Get the value to display for a component, handles radios and basic values.
 */
const getDisplayValue = (component, formData) => {
  if (component.type === "radio") {
    return (
      component.values?.find((v) => v.value === formData[component.key])
        ?.label || formData[component.key]
    );
  }
  return formData[component.key];
};

/**
 * Flatten schema into titled sections with form data merged.
 */
const groupComponentsByTitle = (schema, formData) => {
  const grouped = {};

  const traverse = (components, parentTitle = "General") => {
    for (const component of components) {
      const title = component.title || parentTitle;

      if (component.components) {
        traverse(component.components, title);
      } else if (component.columns) {
        for (const col of component.columns) {
          traverse(col.components || [], title);
        }
      } else if (component.key && component.type !== "htmlelement") {
        if (!grouped[title]) grouped[title] = [];
        grouped[title].push({
          label: component.label,
          displayValue: getDisplayValue(component, formData),
          value: formData[component.key],
          type: component.type,
          key: component.key,
          conditional: component.conditional,
        });
      }
    }
  };

  traverse(schema.components);

  return Object.entries(grouped).map(([title, data]) => ({ title, data }));
};

/**
 * Entry point to read, process, and write cleaned form field data.
 */
const processFormFields = async () => {
  try {
    const raw = await fs.readFile("output.json", "utf8");
    if (!raw) throw new Error("File is empty");

    const parsed = JSON.parse(raw);
    const formData = parsed.formData;
    const bodySchema = JSON.parse(parsed.config?.bodySchema || "{}");

    if (!formData || !bodySchema?.components) {
      throw new Error("Invalid JSON structure or missing fields");
    }

    const grouped = groupComponentsByTitle(bodySchema, formData);
    const cleaned = cleanConditionalFields(grouped);

    await fs.writeFile("formFields.json", JSON.stringify(cleaned, null, 2));
    console.log("✅ Cleaned form fields written to formFields.json");
  } catch (err) {
    console.error("❌ Error:", err.message);
    process.exit(1);
  }
};

// Execute script
processFormFields();
