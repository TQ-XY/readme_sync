---
title: Loyalty Programs
deprecated: false
hidden: false
icon: fad fa-money-bill-1-wave
metadata:
  robots: index
---
## Introduction

The lifecycle of applying a loyalty program to an order follows a clear three-step process, with your system receiving webhooks at each stage.

## Webhooks

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Webhook
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
        [Loyalty Programs](ref:loyalty-programs)
      </td>

      <td>
        <POST_LABEL />
      </td>

      <td>
        This webhook is called to get a list of all loyalty programs a customer is eligible for. Your system should respond with a list of programs, which our channel partners will use to populate a list of available rewards in their user interfaces.
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
        This webhook is called to validate that selected programs are applicable to the current basket. Your system should respond with the specific discounts that should be applied to the order.
      </td>
    </tr>

    <tr>
      <td>
        [Loyalty Order Notification](ref:loyalty-partner-order)
      </td>

      <td>
        <POST_LABEL />
      </td>

      <td>
        This webhook is triggered when an order is finalized and placed or when an order is cancelled.

        When an order is created, your system should handle the automatic redemption of all applied loyalty programs in the basket. This includes deducting loyalty points, marking coupons as used, or processing any other redemption logic.
      </td>
    </tr>

    <tr>
      <td>
        [Cancel Loyalty Order](ref:loyalty-partner-cancel-order)
      </td>

      <td>
        <POST_LABEL />
      </td>

      <td>
        This webhook is triggered when an order is is cancelled.

        For order cancelation, your system should revert any transactions or redemptions that were performed for that order, ensuring that loyalty points are returned and any program usage is undone.
      </td>
    </tr>
  </tbody>
</Table>
