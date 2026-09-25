---
api:
  file: loyalty-api.json
  operationId: loyalty-channel-get-configuration
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
## Purpose

This endpoint provides information on the loyalty platform integrated such as; settings, features and requirements based on the account's configuration.

| Field name                            | Type           | Description                                                                                                                                                                   |
| :------------------------------------ | :------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| enabled                               | bool           | Indicates whether a loyalty provider is active for this channel link.                                                                                                         |
| providerName                          | string         | The display name of the active loyalty provider.                                                                                                                              |
| externalSignUpUrl                     | string \| null | Some providers will only support a external sign-up process. The channel can then redirect customers to this URL.                                                             |
| features                              | object         | Holds information on the features and requirements for the active loyalty provider.                                                                                           |
| features.supportsSSO                  | bool           | Indicates whether the loyalty provider supports SSO.                                                                                                                          |
| features.supportsExternalSignUpUrl    | bool           | Indicates whether the loyalty provider supports external sign-up url.                                                                                                         |
| features.supportsWalletPointsBalance  | bool           | Indicates whether the loyalty provider supports a point-based earning/spending system.                                                                                        |
| features.supportsWalletCashBalance    | bool           | Indicates whether the loyalty provider supports a cash-based earning/spending system.                                                                                         |
| features.supportsBOGOFPrograms        | bool           | Indicates whether the loyalty provider supports buy-one-get-one-free programs.                                                                                                |
| features.supportsFreeItemPrograms     | bool           | Indicates whether the loyalty provider supports free item programs.                                                                                                           |
| features.supportsFlatPrograms         | bool           | Indicates whether the loyalty provider flat-off-order programs                                                                                                                |
| features.requiresEmail                | bool           | Indicates whether the loyalty provider requires this field for creating a user.                                                                                               |
| features.requiresPhoneNumber          | bool           | Indicates whether the loyalty provider requires this field for creating a user.                                                                                               |
| features.supportsDynamicConfiguration | bool           | Indicates whether the loyalty provider is able to retrieve configuration from the loyalty partner at runtime, such as cashback settings, wallet support for cash/points, etc. |
| cashbackConfig                        | CashbackConfig | Contains cashback related configuration. See `CashbackConfig`for more details                                                                                                 |

<br />

### **Table: CashbackConfig**

| Field        | Type                       | Default | Nullable | Description                                 |
| :----------- | :------------------------- | :------ | :------- | :------------------------------------------ |
| title        | String                     | None    | Yes      | The title of the cashback program.          |
| description  | String                     | None    | Yes      | A marketing description of the program.     |
| earningRules | List\[CashbackEarningRule] | \[]     | No       | Rules defining how customers earn rewards.  |
| burningRules | List\[CashbackBurningRule] | \[]     | No       | Rules defining how customers spend rewards. |

<br />

### **Table: CashbackReward**

<Table align={["left","left","left","left","left"]}>
  <thead>
    <tr>
      <th>
        Field
      </th>

      <th>
        Type
      </th>

      <th>
        Default
      </th>

      <th>
        Nullable
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        type
      </td>

      <td>
        String
      </td>

      <td>
        (Required)
      </td>

      <td>
        No
      </td>

      <td>
        Reward type: "percentage" or "fixed".
      </td>
    </tr>

    <tr>
      <td>
        value
      </td>

      <td>
        Integer
      </td>

      <td>
        (Required)
      </td>

      <td>
        No
      </td>

      <td>
        The numeric value of the reward.

        - Fixed amounts: representing the smallest currency unit. Eg. $10.34 will be returned as 1035
        - Percentage amounts: The value for  percentage of 23.43% will be returned as 2343.
      </td>
    </tr>
  </tbody>
</Table>

<br />

### **Table: CashbackEarningRule**

| Field  | Type           | Default    | Nullable | Description                                    |
| :----- | :------------- | :--------- | :------- | :--------------------------------------------- |
| type   | String         | (Required) | No       | Earning type: "cash_back" or "sign_up".        |
| reward | CashbackReward | (Required) | No       | The specific reward associated with this rule. |

<br />

### **Table: CashbackBurningRule**

| Field | Type                                                                | Default    | Nullable | Description                             |
| :---- | :------------------------------------------------------------------ | :--------- | :------- | :-------------------------------------- |
| type  | CashBackBurningRuleType                                             | (Required) | No       | Always purchase.                        |
| cost  | CashbackBurningRuleCostPercentage<br />CashbackBurningRuleCostFixed | (Required) | No       | The cost details (Percentage or Fixed). |

<br />

### **Table: CashbackBurningRuleCostPercentage**

| Field            | Type                   | Default      | Nullable | Description                                        |
| :--------------- | :--------------------- | :----------- | :------- | :------------------------------------------------- |
| type             | Literal ("percentage") | "percentage" | No       | Identifier for percentage-based costs.             |
| value            | Integer                | (Required)   | No       | The percentage value.                              |
| maxBurningAmount | Integer                | None         | Yes      | Maximum amount that can be burned per transaction. |

<br />

### **Table: CashbackBurningRuleCostFixed**

| Field | Type    | Default    | Nullable | Description                        |
| :---- | :------ | :--------- | :------- | :--------------------------------- |
| type  | String  | "fixed"    | No       | Identifier for fixed-amount costs. |
| value | Integer | (Required) | No       | The fixed amount value.            |

<br />