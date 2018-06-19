## App Registrations
> Example POST request:

```shell
curl -s -H "Authorization: Bearer $ACCESS_TOKEN" -H "Content-Type: application/json"
    -XPOST -d '{
        "address_lines": ["123 MAIN ST"],
        "city": "San Mateo",
        "claims_roles": ["billing"],
        "first_name": "Jane",
        "last_name": "Doe",
        "npi": "1234567893"
        "state": "CA",
        "tax_id": ["123456789"],
        "trading_partner_id": "MOCKPAYER",
        "transaction_set_name": "eligibility",
        "zipcode": "99401"
    }' https://platform.pokitdok.com/api/v4/appregistrations
```


```python
params = {
    'address_lines': ['123 MAIN ST'],
    'city': 'San Mateo',
    'claims_roles': ['billing'],
    'first_name': 'Jane',
    'last_name': 'Doe',
    'npi': '1234567893'
    'state': 'CA',
    'tax_id': ['123456789'],
    'trading_partner_id': 'MOCKPAYER',
    'transaction_set_name': 'eligibility',
    'zipcode': '99401'
}
response = pd.post('/appregistrations/', data=params)
```

```csharp
string endpoint = "/appregistrations/";
string method = "POST";
List<string> tax_id = new List<string>;
tax_id.Add("123456789");
List<string> address_lines = new List<string>;
address_lines.Add("123 MAIN ST");
List<string> claims_roles = new List<string>;
claims_roles.Add("billing");
Dictionary<string, object> data = new Dictionary<string, object> {
    {"address_lines": address_lines},
    {"city": "San Mateo"},
    {"claims_roles": claims_roles},
    {"first_name": "Jane"},
    {"last_name": "Doe"},
    {"npi": "1234567893"}
    {"state": "CA"},
    {"tax_id": tax_id},
    {"trading_partner_id": "MOCKPAYER"},
    {"transaction_set_name": "eligibility"},
    {"zipcode": "99401"}
    };
client.request(endpoint, method, data);
```

```ruby
client.request('/appregistrations/', method='post', params={
    address_lines: ['123 MAIN ST'],
    city: 'San Mateo',
    claims_roles: ['billing'],
    first_name: 'Jane',
    last_name: 'Doe',
    npi: '1234567893'
    state: 'CA',
    tax_id: ['123456789'],
    trading_partner_id: 'MOCKPAYER',
    transaction_set_name: 'eligibility',
    zipcode: '99401'
})
```

```swift
let data = [
    "address_lines": ["123 MAIN ST"],
    "city": "San Mateo",
    "claims_roles": ["billing"],
    "first_name": "Jane",
    "last_name": "Doe",
    "npi": "1234567893"
    "state": "CA",
    "tax_id": ["123456789"],
    "trading_partner_id": "MOCKPAYER",
    "transaction_set_name": "eligibility",
    "zipcode": "99401"
] as [String:any]
try client.request(path: "/appregistrations", method: "POST", params: data)
```

> Example response:

```json
{
    "data": {
        "_uuid": "2f201868-47f4-11e8-a91a-0242ac12000a",
        "address_lines": ["123 Main ST"],
        "app_name": "<app_name>",
        "city": "San Mateo",
        "claims_roles": ["billing"],
        "client_id": "<client_id>",
        "first_name": "Jane",
        "last_name": "Doe",
        "npi": "1234567893",
        "state": "CA",
        "tax_id": ["123456789"],
        "trading_partner_id": "MOCKPAYER",
        "transaction_set_name": "eligibility",
        "zipcode": "94401"
    },
    "meta": {
        "...": "..."
    }
}
```

The App Registrations endpoint allows user to manage the NPI registrations associated with their account. These endpoints can be used to create, edit, and delete registrations.

### Endpoint Description

Available Endpoints:

<!--- beginning of table -->
| Endpoint | HTTP Method | Description |
|:---|:---|:---|
| /appregistrations | GET | List current app registrations. |
| /appregistrations/{uuid} | GET | Retrieve the app registration with the given UUID. |
| /appregistrations | POST | Create an app registration. |
| /appregistrations/{uuid} | PUT | Edit the app registration with the given UUID. |
| /appregistrations/{uuid} | DELETE | Delete the app registration with the given UUID. |
| /appregistrations/{uuid}/undelete | POST |Undelete the app registration with the given UUID. |

<!--- end of table -->

### Parameters

The POST `/appregistrations/` and PUT `/appregistrations/` endpoints accept the following parameters:

<!--- beginning of table -->

| Parameter | Type | Description | Presence |
|:---|:---|:---|:--- |
| address_lines | {list} | List of strings representing the street address (e.g. ["123 Main ST.", "Suite 4"]). | Required |
| claims_roles | {list} | List of roles (e.g. 'billing' or 'rendering').| Required |
| city | {string} | The city component of an address (e.g. 'SAN MATEO'). | Required |
| first_name | {string} | Provider's first name. This field should be omitted when sending organization_name. | Situational |
| last_name | {string} | Provider's last name. This field should be omitted when sending organization_name. | Situational |
| npi | {string} | The provider's NPI. | Required |
| organization_name | {string} | The provider's organization name. This field should be omitted when sending first_name and last_name. | Situational |
| state | {string} | The state component of an address (e.g. 'CA'). | Required |
| tax_id | {list} | List of  federal tax ids for the provider. For individual providers, this may be the tax id of the medical practice or organization where a provider works. | Required |
| trading_partner_id| {string} | Unique ID for the intended trading partner, as specified by the [Trading Partners](#trading-partners) endpoint.| Required |
| transaction_set_name | {string} | Transaction this app registration is to be used for (e.g. 'eligibility', 'claims', or 'claim_status'). | Required |
| zipcode | {string} | The zip/postal code (e.g. "94401"). | Required |

<!--- end of table -->

### Response

The `/appregistrations/` response contains the following fields:

<!--- beginning of table -->
| Field | Type | Description |
|:---|:---|:---|
| _uuid | {string} | The unique ID for this app registration.|
| address_lines | {list} | List of strings representing the street address. (e.g. ["123 Main ST.", "Suite 4"]). | Required |
| app_name | {string} | The name of the app associated to the app registration. |
| claims_roles | {list} | List of roles (e.g. 'billing' or 'rendering').| Required |
| city | {string} | The city component of an address (e.g. 'SAN MATEO'). | Required |
| client_id | {string} | The client ID of the app associated to the app registration. |
| first_name | {string} | Provider's first name. |
| last_name | {string} | Provider's last name. |
| npi | {string} | The provider's NPI. |
| organization_name | {string} | The provider's organization name. |
| state | {string} | The state component of an address (e.g. 'CA'). | Required |
| tax_id | {list} | List of  federal tax ids for the provider. For individual providers, this may be the tax id of the medical practice or organization where a provider works. |
| trading_partner_id| {string} | Unique ID for the intended trading partner, as specified by the [Trading Partners](#trading-partners) endpoint.|
| transaction_set_name | {string} | Transaction this app registration is to be used for (e.g. 'eligibility', 'claims', or claim_status). |
| zipcode | {string} | The zip/postal code (e.g. "94401"). | Required |
