---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - json

includes:
  - errors

search: true
---

# Introduction

Welcome to the DentalMock API!

# Authentication

DentalMock uses JWT tokens provided by AWS Cognito to allow access to the API.
Place the token in the Authorization header in order to ensure authentication.

Endpoints that include sensitive data have include additional authorization
that is marked in the docs. 

`Administrator` authentication means that the JWT token must have the user in
thea dmin cognito group in order for the token to be accepted.

`User` authentication means that the JWT token's sub must match the `uid`
provided as a URL parameter in the request.

`Authorization: AWS COGNITO JWS TOKEN`

<aside class="notice">
You must replace <code>AWS COGNITO JWS TOKEN</code> with the session JWT Token.
</aside>



# Patients


## List all patients

> RESPONSE

```json
[
  {
    "_id": {
      "$oid": "DATABASE_GENERATED_ID"
    },
    "appointments": [],
    "created": 1568478669.9997485,
    "email": "USER_EMAIL",
    "messages": [],
    "object": "Patient",
    "profile": {},
    "uid": "AMAZON_COGNITO_SUB"
  },
  {...},
  {...}
]
```

### DESCRIPTION
Returns a list of all of the patients.

### AUTHENTICATION
`Administrator`

### HTTP ENDPOINT
`GET /v1/patients`

### RETURNS
A JSON list with all of your patients as seperate dictionaries. 




## Retrieve a patient

> RESPONSE

```json
{
    "_id": {
      "$oid": "DATABASE_GENERATED_ID"
    },
    "appointments": [],
    "created": 1568478669.9997485,
    "email": "USER_EMAIL",
    "messages": [],
    "object": "Patient",
    "profile": {},
    "uid": "AMS_COGNITO_SUB"
  }
```

### DESCRIPTION
Returns the details of a specific customer. 

### AUTHENTICATION
`User`

### HTTP ENDPOINT
`GET /v1/patients/:uid`

### URL PARAMETERS
Parameter | Description
--------- | -----------
uid | The AWS Cognito SUB found in the JWT token

### RETURNS
JSON dictionary with all of the data inside of the patient object. 




## Create a patient

> POST /v1/patients

```json
{
  "uid": "AMS_COGNITO_SUB",
  "email": "USER_EMAIL"
}
```

> RESPONSE

```json
{
    "_id": {
      "$oid": "DATABASE_GENERATED_ID"
    },
    "appointments": [],
    "created": 1568478669.9997485,
    "email": "USER_EMAIL",
    "messages": [],
    "object": "Patient",
    "profile": {},
    "uid": "AMAZON_COGNITO_SUB"
  }
```

### DESCRIPTION
Creates a new patient inside of the system.

### AUTHENTICATION
`User`

### HTTP ENDPOINT
`POST /v1/patients`

### QUERY PARAMETERS
Parameter | Description
--------- | -----------
uid | The AWS Cognito SUB found in the JWT token
email | The email address associated with the user

### RETURNS
JSON dictionary with the data for that specific patient. It includes a `created`
field which refers to the time in which the patient was created.





## Update a patient

> POST /v1/patients/:uid

```json
{
    "_id": {
      "$oid": "DATABASE_GENERATED_ID"
    },
    "appointments": [],
    "created": 1568478669.9997485,
    "email": "NEW_USER_EMAIL",
    "messages": [],
    "object": "Patient",
    "profile": {},
    "uid": "AMAZON_COGNITO_SUB"
  }
```

> RESPONSE

```json
{
    "_id": {
      "$oid": "DATABASE_GENERATED_ID"
    },
    "appointments": [],
    "created": 1568478669.9997485,
    "email": "NEW_USER_EMAIL",
    "messages": [],
    "object": "Patient",
    "profile": {},
    "uid": "AMAZON_COGNITO_SUB"
  }
```

### DESCRIPTION
Updates a specific patient.

### AUTHENTICATION
`User`

### HTTP ENDPOINT
`POST /v1/patients/:uid`

### URL PARAMETERS
Parameter | Description
--------- | -----------
uid | The AWS Cognito SUB found in the JWT token

### QUERY PARAMETERS
This endpoint requires the entire patient profile object. If you do not have it,
use the other endpoints to retrieve. It can then be updated and sent as the
`JSON body` of this request.

### RETURNS
A JSON dictionary of the patient object which includes the new updates.



## Delete a patient

> RESPONSE

```json
{
   "email": "USER_EMAIL",
   "object": "Patient",
   "deleted": true
}
```
### DESCRIPTION
Deletes a patient from the database.

### AUTHENTICATION
`User`

### HTTP ENDPOINT
`DELETE /v1/patients/:uid`

### URL PARAMETERS
Parameter | Description
--------- | -----------
uid | The AWS Cognito SUB found in the JWT token

### RETURNS
JSON confirmation which contains the patient's `email` and a `deleted` boolean
which will be marked as `True`.




## Retrieve a patient's profile

> RESPONSE

```json
{
  "health": {
    "allergies": "",
    "current_conditions": {
      "acid_reflux": false,
      "anemia": false,
      "arthritis": false,
      "artificial_heart_valve": false,
      "artificial_joints": false,
      "asthma": false,
      "birth_control_pills": false,
      "blood_disease": false,
      "cancer": false,
      "diabetes": false,
      "dizziness": false,
      "epilepsy": false,
      "excessive_bleeding": false,
      "fainting": false,
      "headaches": false,
      "heart_disease": false,
      "hepatitis": false,
      "high_blood_pressure": false,
      "hiv_aids": false,
      "jaw_pain": false,
      "kidney_disease": false,
      "liver_disease": false,
      "mitral_valve_prolapse": false,
      "nursing": false,
      "pacemaker": false,
      "pregnancy": false,
      "radiation_treatment": false,
      "rheumatic_fever": false,
      "shortness_breath": false,
      "sinus_problems": false,
      "stomach_problems": false,
      "stroke": false,
      "swelling_feet": false,
      "thyroid_problems": false,
      "tobacco_habit": false,
      "tonsillitis": false,
      "tuberculosis": false,
      "ulcers": false,
      "venereal_disease": false
    },
    "medications": " "
  },
  "info": {
    "address": {
      "city": "",
      "state": "",
      "street": "",
      "zip": ""
    },
    "date_of_birth": "",
    "email": "",
    "emergency_contact": "",
    "emergency_phone": "",
    "emergency_relation": "",
    "first_name": "",
    "gender": "",
    "home_phone": "",
    "last_name": "",
    "mobile_phone": "",
    "relationship_status": "",
    "work_ext": " ",
    "work_phone": ""
  },
  "insurance": {
    "primary": {
      "employer": {
        "address": {
          "city": "",
          "state": "",
          "street": "",
          "zip": ""
        },
        "name": ""
      },
      "group_number": "",
      "id_number": "",
      "insurer": {
        "name": "",
        "payer_id": ""
      },
      "name_of_insured": {
        "date_of_birth": "",
        "name": "",
        "name_option": "",
        "relation": ""
      },
      "plan": ""
    },
    "secondary": {
      "employer": {
        "address": {
          "city": "",
          "state": "",
          "street": "",
          "zip": ""
        },
        "name": ""
      },
      "group_number": "",
      "id_number": "",
      "insurer": {
        "name": "",
        "payer_id": ""
      },
      "name_of_insured": {
        "date_of_birth": "",
        "name": "",
        "name_option": "",
        "relation": ""
      },
      "plan": ""
    }
  },
  "responsible_party": {
    "address": {
      "city": "",
      "state": "",
      "street": "",
      "zip": ""
    },
    "date_of_birth": "",
    "email": "",
    "first_name": "",
    "gender": "",
    "home_phone": "",
    "last_name": "",
    "mobile_phone": "",
    "relationship_to_patient": "",
    "work_ext": "",
    "work_phone": ""
  }
}
```

### DESCRIPTION
Returns the entire profile of a patient. 

### AUTHENTICATION
`User`

### HTTP ENDPOINT
`GET /v1/patients/:uid/profile`

### URL PARAMETERS
Parameter | Description
--------- | -----------
uid | The AWS Cognito SUB found in the JWT token

### RETURNS
JSON dictionary containing the profile for a patient. 



## Create a patient's profile

> POST /v1/patients/:uid/profile

```json
{
  "health": {
    "allergies": "",
    "current_conditions": {
      "acid_reflux": false,
      "anemia": false,
      "arthritis": false,
      "artificial_heart_valve": false,
      "artificial_joints": false,
      "asthma": false,
      "birth_control_pills": false,
      "blood_disease": false,
      "cancer": false,
      "diabetes": false,
      "dizziness": false,
      "epilepsy": false,
      "excessive_bleeding": false,
      "fainting": false,
      "headaches": false,
      "heart_disease": false,
      "hepatitis": false,
      "high_blood_pressure": false,
      "hiv_aids": false,
      "jaw_pain": false,
      "kidney_disease": false,
      "liver_disease": false,
      "mitral_valve_prolapse": false,
      "nursing": false,
      "pacemaker": false,
      "pregnancy": false,
      "radiation_treatment": false,
      "rheumatic_fever": false,
      "shortness_breath": false,
      "sinus_problems": false,
      "stomach_problems": false,
      "stroke": false,
      "swelling_feet": false,
      "thyroid_problems": false,
      "tobacco_habit": false,
      "tonsillitis": false,
      "tuberculosis": false,
      "ulcers": false,
      "venereal_disease": false
    },
    "medications": " "
  },
  "info": {
    "address": {
      "city": "",
      "state": "",
      "street": "",
      "zip": ""
    },
    "date_of_birth": "",
    "email": "",
    "emergency_contact": "",
    "emergency_phone": "",
    "emergency_relation": "",
    "first_name": "",
    "gender": "",
    "home_phone": "",
    "last_name": "",
    "mobile_phone": "",
    "relationship_status": "",
    "work_ext": " ",
    "work_phone": ""
  },
  "insurance": {
    "primary": {
      "employer": {
        "address": {
          "city": "",
          "state": "",
          "street": "",
          "zip": ""
        },
        "name": ""
      },
      "group_number": "",
      "id_number": "",
      "insurer": {
        "name": "",
        "payer_id": ""
      },
      "name_of_insured": {
        "date_of_birth": "",
        "name": "",
        "name_option": "",
        "relation": ""
      },
      "plan": ""
    },
    "secondary": {
      "employer": {
        "address": {
          "city": "",
          "state": "",
          "street": "",
          "zip": ""
        },
        "name": ""
      },
      "group_number": "",
      "id_number": "",
      "insurer": {
        "name": "",
        "payer_id": ""
      },
      "name_of_insured": {
        "date_of_birth": "",
        "name": "",
        "name_option": "",
        "relation": ""
      },
      "plan": ""
    }
  },
  "responsible_party": {
    "address": {
      "city": "",
      "state": "",
      "street": "",
      "zip": ""
    },
    "date_of_birth": "",
    "email": "",
    "first_name": "",
    "gender": "",
    "home_phone": "",
    "last_name": "",
    "mobile_phone": "",
    "relationship_to_patient": "",
    "work_ext": "",
    "work_phone": ""
  }
}
```

> RESPONSE

```json
{
    "_id": {
      "$oid": "DATABASE_GENERATED_ID"
    },
    "appointments": [],
    "created": 1568478669.9997485,
    "email": "USER_EMAIL",
    "messages": [],
    "object": "Patient",
    "profile": {
      "health": {
        "allergies": "",
        "current_conditions": {
          "acid_reflux": false,
          "anemia": false,
          "arthritis": false,
          "artificial_heart_valve": false,
          "artificial_joints": false,
          "asthma": false,
          "birth_control_pills": false,
          "blood_disease": false,
          "cancer": false,
          "diabetes": false,
          "dizziness": false,
          "epilepsy": false,
          "excessive_bleeding": false,
          "fainting": false,
          "headaches": false,
          "heart_disease": false,
          "hepatitis": false,
          "high_blood_pressure": false,
          "hiv_aids": false,
          "jaw_pain": false,
          "kidney_disease": false,
          "liver_disease": false,
          "mitral_valve_prolapse": false,
          "nursing": false,
          "pacemaker": false,
          "pregnancy": false,
          "radiation_treatment": false,
          "rheumatic_fever": false,
          "shortness_breath": false,
          "sinus_problems": false,
          "stomach_problems": false,
          "stroke": false,
          "swelling_feet": false,
          "thyroid_problems": false,
          "tobacco_habit": false,
          "tonsillitis": false,
          "tuberculosis": false,
          "ulcers": false,
          "venereal_disease": false
        },
        "medications": " "
      },
      "info": {
        "address": {
          "city": "",
          "state": "",
          "street": "",
          "zip": ""
        },
        "date_of_birth": "",
        "email": "",
        "emergency_contact": "",
        "emergency_phone": "",
        "emergency_relation": "",
        "first_name": "",
        "gender": "",
        "home_phone": "",
        "last_name": "",
        "mobile_phone": "",
        "relationship_status": "",
        "work_ext": " ",
        "work_phone": ""
      },
      "insurance": {
        "primary": {
          "employer": {
            "address": {
              "city": "",
              "state": "",
              "street": "",
              "zip": ""
            },
            "name": ""
          },
          "group_number": "",
          "id_number": "",
          "insurer": {
            "name": "",
            "payer_id": ""
          },
          "name_of_insured": {
            "date_of_birth": "",
            "name": "",
            "name_option": "",
            "relation": ""
          },
          "plan": ""
        },
        "secondary": {
          "employer": {
            "address": {
              "city": "",
              "state": "",
              "street": "",
              "zip": ""
            },
            "name": ""
          },
          "group_number": "",
          "id_number": "",
          "insurer": {
            "name": "",
            "payer_id": ""
          },
          "name_of_insured": {
            "date_of_birth": "",
            "name": "",
            "name_option": "",
            "relation": ""
          },
          "plan": ""
        }
      },
      "responsible_party": {
        "address": {
          "city": "",
          "state": "",
          "street": "",
          "zip": ""
        },
        "date_of_birth": "",
        "email": "",
        "first_name": "",
        "gender": "",
        "home_phone": "",
        "last_name": "",
        "mobile_phone": "",
        "relationship_to_patient": "",
        "work_ext": "",
        "work_phone": ""
      }
    },
    "uid": "AMS_COGNITO_SUB"
  }
```


### DESCRIPTION
Creates a profile for a specific patient.

### AUTHENTICATION
`User`

### HTTP ENDPOINT
`POST /v1/patients/:uid/profile`

### URL PARAMETERS
Parameter | Description
--------- | -----------
uid | The AWS Cognito SUB found in the JWT token

### QUERY PARAMETERS
Requries the entire profile object. The example `POST JSON` can be used to test
with.

### RETURNS
The patient object as a `JSON` dictionary. It contains the new patient profile
under the `profile` key.



## Update a patient's profile

> POST /v1/patients/:uid/profile

```json
{
  "health": {
    "allergies": "",
    "current_conditions": {
      "acid_reflux": false,
      "anemia": false,
      "arthritis": false,
      "artificial_heart_valve": false,
      "artificial_joints": false,
      "asthma": false,
      "birth_control_pills": false,
      "blood_disease": false,
      "cancer": false,
      "diabetes": false,
      "dizziness": false,
      "epilepsy": false,
      "excessive_bleeding": false,
      "fainting": false,
      "headaches": false,
      "heart_disease": false,
      "hepatitis": false,
      "high_blood_pressure": false,
      "hiv_aids": false,
      "jaw_pain": false,
      "kidney_disease": false,
      "liver_disease": false,
      "mitral_valve_prolapse": false,
      "nursing": false,
      "pacemaker": false,
      "pregnancy": false,
      "radiation_treatment": false,
      "rheumatic_fever": false,
      "shortness_breath": false,
      "sinus_problems": false,
      "stomach_problems": false,
      "stroke": false,
      "swelling_feet": false,
      "thyroid_problems": false,
      "tobacco_habit": false,
      "tonsillitis": false,
      "tuberculosis": false,
      "ulcers": false,
      "venereal_disease": false
    },
    "medications": " "
  },
  "info": {
    "address": {
      "city": "",
      "state": "",
      "street": "",
      "zip": ""
    },
    "date_of_birth": "",
    "email": "",
    "emergency_contact": "",
    "emergency_phone": "",
    "emergency_relation": "",
    "first_name": "",
    "gender": "",
    "home_phone": "",
    "last_name": "",
    "mobile_phone": "",
    "relationship_status": "",
    "work_ext": " ",
    "work_phone": ""
  },
  "insurance": {
    "primary": {
      "employer": {
        "address": {
          "city": "",
          "state": "",
          "street": "",
          "zip": ""
        },
        "name": ""
      },
      "group_number": "",
      "id_number": "",
      "insurer": {
        "name": "",
        "payer_id": ""
      },
      "name_of_insured": {
        "date_of_birth": "",
        "name": "",
        "name_option": "",
        "relation": ""
      },
      "plan": ""
    },
    "secondary": {
      "employer": {
        "address": {
          "city": "",
          "state": "",
          "street": "",
          "zip": ""
        },
        "name": ""
      },
      "group_number": "",
      "id_number": "",
      "insurer": {
        "name": "",
        "payer_id": ""
      },
      "name_of_insured": {
        "date_of_birth": "",
        "name": "",
        "name_option": "",
        "relation": ""
      },
      "plan": ""
    }
  },
  "responsible_party": {
    "address": {
      "city": "",
      "state": "",
      "street": "",
      "zip": ""
    },
    "date_of_birth": "",
    "email": "",
    "first_name": "",
    "gender": "",
    "home_phone": "",
    "last_name": "",
    "mobile_phone": "",
    "relationship_to_patient": "",
    "work_ext": "",
    "work_phone": ""
  }
}
```

> RESPONSE

```json
{
    "_id": {
      "$oid": "DATABASE_GENERATED_ID"
    },
    "appointments": [],
    "created": 1568478669.9997485,
    "email": "USER_EMAIL",
    "messages": [],
    "object": "Patient",
    "profile": {
      "health": {
        "allergies": "",
        "current_conditions": {
          "acid_reflux": false,
          "anemia": false,
          "arthritis": false,
          "artificial_heart_valve": false,
          "artificial_joints": false,
          "asthma": false,
          "birth_control_pills": false,
          "blood_disease": false,
          "cancer": false,
          "diabetes": false,
          "dizziness": false,
          "epilepsy": false,
          "excessive_bleeding": false,
          "fainting": false,
          "headaches": false,
          "heart_disease": false,
          "hepatitis": false,
          "high_blood_pressure": false,
          "hiv_aids": false,
          "jaw_pain": false,
          "kidney_disease": false,
          "liver_disease": false,
          "mitral_valve_prolapse": false,
          "nursing": false,
          "pacemaker": false,
          "pregnancy": false,
          "radiation_treatment": false,
          "rheumatic_fever": false,
          "shortness_breath": false,
          "sinus_problems": false,
          "stomach_problems": false,
          "stroke": false,
          "swelling_feet": false,
          "thyroid_problems": false,
          "tobacco_habit": false,
          "tonsillitis": false,
          "tuberculosis": false,
          "ulcers": false,
          "venereal_disease": false
        },
        "medications": " "
      },
      "info": {
        "address": {
          "city": "",
          "state": "",
          "street": "",
          "zip": ""
        },
        "date_of_birth": "",
        "email": "",
        "emergency_contact": "",
        "emergency_phone": "",
        "emergency_relation": "",
        "first_name": "",
        "gender": "",
        "home_phone": "",
        "last_name": "",
        "mobile_phone": "",
        "relationship_status": "",
        "work_ext": " ",
        "work_phone": ""
      },
      "insurance": {
        "primary": {
          "employer": {
            "address": {
              "city": "",
              "state": "",
              "street": "",
              "zip": ""
            },
            "name": ""
          },
          "group_number": "",
          "id_number": "",
          "insurer": {
            "name": "",
            "payer_id": ""
          },
          "name_of_insured": {
            "date_of_birth": "",
            "name": "",
            "name_option": "",
            "relation": ""
          },
          "plan": ""
        },
        "secondary": {
          "employer": {
            "address": {
              "city": "",
              "state": "",
              "street": "",
              "zip": ""
            },
            "name": ""
          },
          "group_number": "",
          "id_number": "",
          "insurer": {
            "name": "",
            "payer_id": ""
          },
          "name_of_insured": {
            "date_of_birth": "",
            "name": "",
            "name_option": "",
            "relation": ""
          },
          "plan": ""
        }
      },
      "responsible_party": {
        "address": {
          "city": "",
          "state": "",
          "street": "",
          "zip": ""
        },
        "date_of_birth": "",
        "email": "",
        "first_name": "",
        "gender": "",
        "home_phone": "",
        "last_name": "",
        "mobile_phone": "",
        "relationship_to_patient": "",
        "work_ext": "",
        "work_phone": ""
      }
    },
    "uid": "AMS_COGNITO_SUB"
  }
```

### DESCRIPTION
Updates the entire profile for a specific patient.

### AUTHENTICATION
`User`

### HTTP ENDPOINT
`POST /v1/patients/:uid/profile`

### URL PARAMETERS
Parameter | Description
--------- | -----------
uid | The AWS Cognito SUB found in the JWT token

### QUERY PARAMETERS
Requries the entire profile object. If you do not have it, use the other 
endpoints to retrieve it. Once edited, provide the entire object in the 
`POST request`.

### RETURNS
The patient object as a `JSON` dictionary. It contains the newly updated patient
profile under the `profile` key.



## Retrieve patient's profile section

> RESPONSE FOR INFO

```json
{
    "address": {
      "city": "",
      "state": "",
      "street": "",
      "zip": ""
    },
    "date_of_birth": "",
    "email": "",
    "emergency_contact": "",
    "emergency_phone": "",
    "emergency_relation": "",
    "first_name": "",
    "gender": "",
    "home_phone": "",
    "last_name": "",
    "mobile_phone": "",
    "relationship_status": "",
    "work_ext": " ",
    "work_phone": ""
}
```

> RESPONSE FOR RESPONSIBLE PARTY

```json
{
    "address": {
      "city": "",
      "state": "",
      "street": "",
      "zip": ""
    },
    "date_of_birth": "",
    "email": "",
    "first_name": "",
    "gender": "",
    "home_phone": "",
    "last_name": "",
    "mobile_phone": "",
    "relationship_to_patient": "",
    "work_ext": "",
    "work_phone": ""
  }
}
```

> RESPONSE FOR INSURANCE

```json
{
    "primary": {
      "employer": {
        "address": {
          "city": "",
          "state": "",
          "street": "",
          "zip": ""
        },
        "name": ""
      },
      "group_number": "",
      "id_number": "",
      "insurer": {
        "name": "",
        "payer_id": ""
      },
      "name_of_insured": {
        "date_of_birth": "",
        "name": "",
        "name_option": "",
        "relation": ""
      },
      "plan": ""
    },
    "secondary": {
      "employer": {
        "address": {
          "city": "",
          "state": "",
          "street": "",
          "zip": ""
        },
        "name": ""
      },
      "group_number": "",
      "id_number": "",
      "insurer": {
        "name": "",
        "payer_id": ""
      },
      "name_of_insured": {
        "date_of_birth": "",
        "name": "",
        "name_option": "",
        "relation": ""
      },
      "plan": ""
    }
 }
```

> RESPONSE FOR HEALTH

```json
{
    "allergies": "",
    "current_conditions": {
      "acid_reflux": false,
      "anemia": false,
      "arthritis": false,
      "artificial_heart_valve": false,
      "artificial_joints": false,
      "asthma": false,
      "birth_control_pills": false,
      "blood_disease": false,
      "cancer": false,
      "diabetes": false,
      "dizziness": false,
      "epilepsy": false,
      "excessive_bleeding": false,
      "fainting": false,
      "headaches": false,
      "heart_disease": false,
      "hepatitis": false,
      "high_blood_pressure": false,
      "hiv_aids": false,
      "jaw_pain": false,
      "kidney_disease": false,
      "liver_disease": false,
      "mitral_valve_prolapse": false,
      "nursing": false,
      "pacemaker": false,
      "pregnancy": false,
      "radiation_treatment": false,
      "rheumatic_fever": false,
      "shortness_breath": false,
      "sinus_problems": false,
      "stomach_problems": false,
      "stroke": false,
      "swelling_feet": false,
      "thyroid_problems": false,
      "tobacco_habit": false,
      "tonsillitis": false,
      "tuberculosis": false,
      "ulcers": false,
      "venereal_disease": false
    },
    "medications": " "
}
```

### DESCRIPTION
Returns a specific section of a patient's profile.

### HTTP ENDPOINT
`GET /v1/patients/:uid/profile/:section`

### AUTHENTICATION
`User`

### URL PARAMETERS
Parameter | Description
--------- | -----------
uid | The AWS Cognito SUB found in the JWT token
section | info
        | responsible_party
        | insurance
        | health

### RETURNS
The specific section as a `JSON` dictionary. 



## Update a patient's profile section

> POST /v1/patients/:uid/profile/info

```json
{
    "address": {
      "city": "",
      "state": "",
      "street": "",
      "zip": ""
    },
    "date_of_birth": "",
    "email": "",
    "emergency_contact": "",
    "emergency_phone": "",
    "emergency_relation": "",
    "first_name": "",
    "gender": "",
    "home_phone": "",
    "last_name": "",
    "mobile_phone": "",
    "relationship_status": "",
    "work_ext": " ",
    "work_phone": ""
}
```

> POST /v1/patients/:uid/profile/responsible_party

```json
{
    "address": {
      "city": "",
      "state": "",
      "street": "",
      "zip": ""
    },
    "date_of_birth": "",
    "email": "",
    "first_name": "",
    "gender": "",
    "home_phone": "",
    "last_name": "",
    "mobile_phone": "",
    "relationship_to_patient": "",
    "work_ext": "",
    "work_phone": ""
  }
}
```

> POST /v1/patients/:uid/profile/insurance

```json
{
    "primary": {
      "employer": {
        "address": {
          "city": "",
          "state": "",
          "street": "",
          "zip": ""
        },
        "name": ""
      },
      "group_number": "",
      "id_number": "",
      "insurer": {
        "name": "",
        "payer_id": ""
      },
      "name_of_insured": {
        "date_of_birth": "",
        "name": "",
        "name_option": "",
        "relation": ""
      },
      "plan": ""
    },
    "secondary": {
      "employer": {
        "address": {
          "city": "",
          "state": "",
          "street": "",
          "zip": ""
        },
        "name": ""
      },
      "group_number": "",
      "id_number": "",
      "insurer": {
        "name": "",
        "payer_id": ""
      },
      "name_of_insured": {
        "date_of_birth": "",
        "name": "",
        "name_option": "",
        "relation": ""
      },
      "plan": ""
    }
 }
```

> POST /v1/patients/:uid/profile/health

```json
{
    "allergies": "",
    "current_conditions": {
      "acid_reflux": false,
      "anemia": false,
      "arthritis": false,
      "artificial_heart_valve": false,
      "artificial_joints": false,
      "asthma": false,
      "birth_control_pills": false,
      "blood_disease": false,
      "cancer": false,
      "diabetes": false,
      "dizziness": false,
      "epilepsy": false,
      "excessive_bleeding": false,
      "fainting": false,
      "headaches": false,
      "heart_disease": false,
      "hepatitis": false,
      "high_blood_pressure": false,
      "hiv_aids": false,
      "jaw_pain": false,
      "kidney_disease": false,
      "liver_disease": false,
      "mitral_valve_prolapse": false,
      "nursing": false,
      "pacemaker": false,
      "pregnancy": false,
      "radiation_treatment": false,
      "rheumatic_fever": false,
      "shortness_breath": false,
      "sinus_problems": false,
      "stomach_problems": false,
      "stroke": false,
      "swelling_feet": false,
      "thyroid_problems": false,
      "tobacco_habit": false,
      "tonsillitis": false,
      "tuberculosis": false,
      "ulcers": false,
      "venereal_disease": false
    },
    "medications": " "
}
```

> RESPONSE

```json
{
    "_id": {
      "$oid": "DATABASE_GENERATED_ID"
    },
    "appointments": [],
    "created": 1568478669.9997485,
    "email": "USER_EMAIL",
    "messages": [],
    "object": "Patient",
    "profile": {
      "health": {
        "allergies": "",
        "current_conditions": {
          "acid_reflux": false,
          "anemia": false,
          "arthritis": false,
          "artificial_heart_valve": false,
          "artificial_joints": false,
          "asthma": false,
          "birth_control_pills": false,
          "blood_disease": false,
          "cancer": false,
          "diabetes": false,
          "dizziness": false,
          "epilepsy": false,
          "excessive_bleeding": false,
          "fainting": false,
          "headaches": false,
          "heart_disease": false,
          "hepatitis": false,
          "high_blood_pressure": false,
          "hiv_aids": false,
          "jaw_pain": false,
          "kidney_disease": false,
          "liver_disease": false,
          "mitral_valve_prolapse": false,
          "nursing": false,
          "pacemaker": false,
          "pregnancy": false,
          "radiation_treatment": false,
          "rheumatic_fever": false,
          "shortness_breath": false,
          "sinus_problems": false,
          "stomach_problems": false,
          "stroke": false,
          "swelling_feet": false,
          "thyroid_problems": false,
          "tobacco_habit": false,
          "tonsillitis": false,
          "tuberculosis": false,
          "ulcers": false,
          "venereal_disease": false
        },
        "medications": " "
      },
      "info": {
        "address": {
          "city": "",
          "state": "",
          "street": "",
          "zip": ""
        },
        "date_of_birth": "",
        "email": "",
        "emergency_contact": "",
        "emergency_phone": "",
        "emergency_relation": "",
        "first_name": "",
        "gender": "",
        "home_phone": "",
        "last_name": "",
        "mobile_phone": "",
        "relationship_status": "",
        "work_ext": " ",
        "work_phone": ""
      },
      "insurance": {
        "primary": {
          "employer": {
            "address": {
              "city": "",
              "state": "",
              "street": "",
              "zip": ""
            },
            "name": ""
          },
          "group_number": "",
          "id_number": "",
          "insurer": {
            "name": "",
            "payer_id": ""
          },
          "name_of_insured": {
            "date_of_birth": "",
            "name": "",
            "name_option": "",
            "relation": ""
          },
          "plan": ""
        },
        "secondary": {
          "employer": {
            "address": {
              "city": "",
              "state": "",
              "street": "",
              "zip": ""
            },
            "name": ""
          },
          "group_number": "",
          "id_number": "",
          "insurer": {
            "name": "",
            "payer_id": ""
          },
          "name_of_insured": {
            "date_of_birth": "",
            "name": "",
            "name_option": "",
            "relation": ""
          },
          "plan": ""
        }
      },
      "responsible_party": {
        "address": {
          "city": "",
          "state": "",
          "street": "",
          "zip": ""
        },
        "date_of_birth": "",
        "email": "",
        "first_name": "",
        "gender": "",
        "home_phone": "",
        "last_name": "",
        "mobile_phone": "",
        "relationship_to_patient": "",
        "work_ext": "",
        "work_phone": ""
      }
    },
    "uid": "AMS_COGNITO_SUB"
  }
```


### DESCRIPTION
Updates a specific section of a patient's profile.

### HTTP ENDPOINT
`POST /v1/patients/:uid/profile/:section`

### AUTHENTICATION
`User`

### URL PARAMETERS
Parameter | Description
--------- | -----------
uid | The AWS Cognito SUB found in the JWT token
section | info
        | responsible_party
        | insurance
        | health

### RETURNS
The entire patient object as a `JSON` dictionary. It includes the newly updated
data.



## Retrieve a patient's messages

> RESPONSE

```json
[
    {
    "created": 1568647703.4027293,
    "dentist": "",
    "text": ""
    },
    {...},
    {...}
]
```

### DESCRIPTION
Returns a list of a patient's messages

### HTTP ENDPOINT
`GET /v1/patients/:uid/messages`

### AUTHENTICATION
`User`

### URL PARAMETERS
Parameter | Description
--------- | -----------
uid | The AWS Cognito SUB found in the JWT token

### RETURNS
A `JSON` list of a patient's messages.


## Create a patient's message

> POST /v1/patients/:uid/messages

```json
{
    "dentist": "",
    "text": ""
}
``` 

> RESPONSE

```json
{
    "_id": {
      "$oid": "DATABASE_GENERATED_ID"
    },
    "appointments": [],
    "created": 1568478669.9997485,
    "email": "USER_EMAIL",
    "messages": [
        {
            "dentist": "",
            "text": ""
        }
    ],
    "object": "Patient",
    "profile": {
      "health": {
        "allergies": "",
        "current_conditions": {
          "acid_reflux": false,
          "anemia": false,
          "arthritis": false,
          "artificial_heart_valve": false,
          "artificial_joints": false,
          "asthma": false,
          "birth_control_pills": false,
          "blood_disease": false,
          "cancer": false,
          "diabetes": false,
          "dizziness": false,
          "epilepsy": false,
          "excessive_bleeding": false,
          "fainting": false,
          "headaches": false,
          "heart_disease": false,
          "hepatitis": false,
          "high_blood_pressure": false,
          "hiv_aids": false,
          "jaw_pain": false,
          "kidney_disease": false,
          "liver_disease": false,
          "mitral_valve_prolapse": false,
          "nursing": false,
          "pacemaker": false,
          "pregnancy": false,
          "radiation_treatment": false,
          "rheumatic_fever": false,
          "shortness_breath": false,
          "sinus_problems": false,
          "stomach_problems": false,
          "stroke": false,
          "swelling_feet": false,
          "thyroid_problems": false,
          "tobacco_habit": false,
          "tonsillitis": false,
          "tuberculosis": false,
          "ulcers": false,
          "venereal_disease": false
        },
        "medications": " "
      },
      "info": {
        "address": {
          "city": "",
          "state": "",
          "street": "",
          "zip": ""
        },
        "date_of_birth": "",
        "email": "",
        "emergency_contact": "",
        "emergency_phone": "",
        "emergency_relation": "",
        "first_name": "",
        "gender": "",
        "home_phone": "",
        "last_name": "",
        "mobile_phone": "",
        "relationship_status": "",
        "work_ext": " ",
        "work_phone": ""
      },
      "insurance": {
        "primary": {
          "employer": {
            "address": {
              "city": "",
              "state": "",
              "street": "",
              "zip": ""
            },
            "name": ""
          },
          "group_number": "",
          "id_number": "",
          "insurer": {
            "name": "",
            "payer_id": ""
          },
          "name_of_insured": {
            "date_of_birth": "",
            "name": "",
            "name_option": "",
            "relation": ""
          },
          "plan": ""
        },
        "secondary": {
          "employer": {
            "address": {
              "city": "",
              "state": "",
              "street": "",
              "zip": ""
            },
            "name": ""
          },
          "group_number": "",
          "id_number": "",
          "insurer": {
            "name": "",
            "payer_id": ""
          },
          "name_of_insured": {
            "date_of_birth": "",
            "name": "",
            "name_option": "",
            "relation": ""
          },
          "plan": ""
        }
      },
      "responsible_party": {
        "address": {
          "city": "",
          "state": "",
          "street": "",
          "zip": ""
        },
        "date_of_birth": "",
        "email": "",
        "first_name": "",
        "gender": "",
        "home_phone": "",
        "last_name": "",
        "mobile_phone": "",
        "relationship_to_patient": "",
        "work_ext": "",
        "work_phone": ""
      }
    },
    "uid": "AMS_COGNITO_SUB"
  }
```


### DESCRIPTION
Creates a new message for a patient that the dentist will be able to read and
response too.

### HTTP ENDPOINT
`POST /v1/patients/:uid/messages`

### AUTHENTICATION
`User`

### URL PARAMETERS
Parameter | Description
--------- | -----------
uid | The AWS Cognito SUB found in the JWT token

### QUERY PARAMETERS
The entire message object is required as a `JSON POST request`.

### RETURNS
A `JSON` dictionary of the entire patient object. It includes the newly created
message.


