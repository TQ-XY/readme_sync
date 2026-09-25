---
title: Endpoints
deprecated: false
hidden: false
icon: fad fa-plug
metadata:
  robots: index
---
<BaseURLsTable />

# Configuration Endpoints

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Endpoint
      </th>

      <th>
        Method
      </th>

      <th>
        Purpose
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        [Get Loyalty Configuration](ref:loyalty-channel-get-configuration)
      </td>

      <td>
        <GET_LABEL />
      </td>

      <td>
        Returns information on the current loyalty configuration.
      </td>
    </tr>
  </tbody>
</Table>

# Customer Management Endpoints

The following endpoints are available for managing customer information and loyalty data.

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Endpoint
      </th>

      <th>
        Method
      </th>

      <th>
        Purpose
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        [Create Loyalty Customer](ref:loyalty-channel-create-loyalty-customer)
      </td>

      <td>
        <POST_LABEL />
      </td>

      <td>
        This endpoint is used to create a customer profile. It allows a channel to send customer information (such as name, email, and phone number) to the loyalty provider.
      </td>
    </tr>

    <tr>
      <td>
        [Get Loyalty Customer](ref:loyalty-channel-get-customer)
      </td>

      <td>
        <GET_LABEL />
      </td>

      <td>
        This endpoint is used to retrieve a customer's profile details. A channel can call this endpoint to fetch a customer's information, including their loyalty customer ID and other relevant profile data. This is essential for subsequent API calls that require the customer's unique loyalty ID.
      </td>
    </tr>
  </tbody>
</Table>

# Tier System Endpoint

The tier system allows loyalty providers to define and manage customer loyalty tiers based on criteria such as lifetime points. Channels can use the following endpoint to retrieve a list of all available tiers and their requirements, enabling them to display a customer's progress and the benefits of reaching higher tiers.

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Endpoint
      </th>

      <th>
        Method
      </th>

      <th>
        Purpose
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        [Get Loyalty Tiers](ref:loyalty_tiers)
      </td>

      <td>
        <GET_LABEL />
      </td>

      <td>
        This endpoint is used to retrieve a list of all available loyalty tiers. The response includes details about each tier, such as its name, a description, and the point requirements to achieve it. This information is valuable for building a user interface that visualizes a customer's current tier status and motivates them to earn more points to reach the next level.
      </td>
    </tr>
  </tbody>
</Table>

<br />

# Wallet Application Lifecycle

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Endpoint
      </th>

      <th>
        Method
      </th>

      <th>
        Purpose
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        [Get Loyalty Customer Wallet](ref:get-loyalty-customer-wallet)
      </td>

      <td>
        <GET_LABEL />
      </td>

      <td>
        This endpoint is used to retrieve a customer's wallet balance. It provides the channel with the customer's available funds in the form of cash and/or loyalty points. This allows the channel to display the customer's current balance, enabling them to make informed decisions about using their rewards. This endpoint is crucial for functionalities such as "pay with points" or showing a customer's current points balance on the application's user interface.
      </td>
    </tr>
  </tbody>
</Table>

# Program Application Lifecycle

During the program application lifecycle, you will need to provide a `sessionId`, which is a unique token that you generate and maintain to link all customer actions throughout the loyalty program lifecycle.

You must provide the same `sessionId` for all calls to get programs, validate programs, and the create order request. Using a consistent `sessionId` ensures a single, continuous customer journey is followed, which helps loyalty partners prevent fraudulent activity.

Once the customer has placed the order, the session is considered complete. The `sessionId` used during that process should no longer be used for new loyalty interactions.

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Endpoint
      </th>

      <th>
        Method
      </th>

      <th>
        Purpose
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        [Get Loyalty Programs](ref:loyalty-channel-get-programs)
      </td>

      <td>
        <POST_LABEL />
      </td>

      <td>
        The channel calls this endpoint to get a list of all loyalty programs a customer is eligible for. This is typically done to populate a list of available programs in the user interface.
      </td>
    </tr>

    <tr>
      <td>
        [Validate Programs](ref:loyalty-platform-validate-program)
      </td>

      <td>
        <POST_LABEL />
      </td>

      <td>
        As the customer builds their order, the channel calls this endpoint to validate that selected programs are applicable to the current basket. The response will indicate which discounts should be applied.
      </td>
    </tr>
  </tbody>
</Table>
