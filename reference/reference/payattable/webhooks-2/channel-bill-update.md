---
api:
  file: payattable-webhooks.json
  operationId: get_new-endpoint-1
hidden: true
link:
  new_tab: false
metadata:
  robots: index
---
<HTMLBlock>{`
<div style="background: #F00; font-weight: bold; color: #FFF; padding: 10px">Please do not yet share this information to anyone else.<br>The below spec might still be prone to changes.</div>
`}</HTMLBlock>

This webhook is called when we retrieved an updated version of the bill following on the request you made via [GET Bill by ID](ref:bill-by-id) or [GET Bills by Table](ref:bills-by-table) .

## What we will send you

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Field name
      </th>

      <th>
        Type
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        callbackId
      </td>

      <td>
        string
      </td>

      <td>
        Unique ID that was communicated to you upon calling [GET Bill by ID](ref:bill-by-id) or [GET Bills by Table](ref:bills-by-table). This enables you to link your initial request to the asynchronous webhook call you get from us.
      </td>
    </tr>

    <tr>
      <td>
        bills
      </td>

      <td>
        array of objects
      </td>

      <td>
        An array of bills matching your previous request, but possibly containing updates. The structure of the bill is the same as the one you can find in [GET Bill by ID](ref:bill-by-id).

        Regardless of the initial call being [GET Bill by ID](ref:bill-by-id) or [GET Bills by Table](ref:bills-by-table), we will return an array. In the case of [GET Bill by ID](ref:bill-by-id) , the array would contain one bill.
      </td>
    </tr>
  </tbody>
</Table>