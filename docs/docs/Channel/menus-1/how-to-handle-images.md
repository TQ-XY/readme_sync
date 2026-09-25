---
title: How to handle Images
deprecated: false
hidden: false
link:
  new_tab: false
metadata:
  robots: index
---
## Introduction

A published menu can contain image URLs for each of the following attributes;

| Item                | Key                        | Description                                                   |
| :------------------ | :------------------------- | :------------------------------------------------------------ |
| **Menu**            | `"menuImageURL"`           | The menu itself can have a hero/banner image set              |
| **Categories**      | "categories.`imageUrl`"    | Each category can have it's own image                         |
| **Products**        | "products.`imageUrl`"      | Each product can have it's own image                          |
| **Modifier**        | "modifiers`imageUrl`"      | In certain cases, modifiers can have an associated image      |
| **Modifier Groups** | "modifierGroups`imageUrl`" | In very specific use cases, modifier groups can have an image |

Deliverect will host images synced from a POS system or uploaded by a user (more info on manual upload [here](https://help.deliverect.com/en/articles/7979042-add-images-to-your-media-page))

Hosted images will be sent as a URL like the example below;

<HTMLBlock>{`
<div style="font-family: monospace; line-height: 2.4;">
  <span style="background:#E8F5EE; color:#276B47; padding:4px 7px; border-radius:5px;">https://resizer.staging.deliverect.com</span>
  <span style="color:#3E8C5F; font-weight:bold; padding:0 4px;">/</span>

  <span style="background:#F1F5F3; color:#333; padding:4px 7px; border-radius:5px;">-2NUaOqszu...</span>
  <span style="color:#3E8C5F; font-weight:bold; padding:0 4px;">/</span>

  <span style="background:#E8F5EE; color:#276B47; padding:4px 7px; border-radius:5px;">rt:fill/g:ce/el:0</span>
  <span style="color:#3E8C5F; font-weight:bold; padding:0 4px;">/</span>

  <span style="background:#F1F5F3; color:#333; padding:4px 7px; border-radius:5px;">cb:d74d2dae7c414232a...</span>
  <span style="color:#3E8C5F; font-weight:bold; padding:0 4px;">/</span>

  <span style="background:#FFF4D6; color:#795B00; padding:4px 7px; border-radius:5px;">aHR0cHM6Ly9kZ...</span>
  <span style="color:#3E8C5F; font-weight:bold; padding:0 4px;">/</span>

  <span style="background:#F1F5F3; color:#333; padding:4px 7px; border-radius:5px;">.jpg</span>
</div>
`}</HTMLBlock>

| Segment                                                                                                                                                                                               | Description                                |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------ |
| <span style="background:#E8F5EE; color:#276B47; padding:4px 7px; border-radius:5px; font-family:monospace;">[https://resizer.staging.deliverect.com/](https://resizer.staging.deliverect.com/)</span> | **Base URL** of our image resizer          |
| <span style="background:#F1F5F3; color:#333; padding:4px 7px; border-radius:5px; font-family:monospace;">`-2NUaOqszu...`/</span>                                                                      | **Unique ID** of image                     |
| <span style="background:#E8F5EE; color:#276B47; padding:4px 7px; border-radius:5px; font-family:monospace;">rt:fill/g:ce/el:0/</span>                                                                 | **Rendering parameters**                   |
| <span style="background:#F1F5F3; color:#333; padding:4px 7px; border-radius:5px; font-family:monospace;">cb:d74d2dae7c414232a7d4558ef4678ecb/</span>                                                  | **Cache buster**                           |
| <span style="background:#FFF4D6; color:#795B00; padding:4px 7px; border-radius:5px; font-family:monospace;">`aHR0cHM6Ly9kZ...`</span>                                                                 | **Base64 encoding** for original image URL |
| <span style="background:#F1F5F3; color:#333; padding:4px 7px; border-radius:5px; font-family:monospace;">.jpg</span>                                                                                  | **Image format**                           |

## Maintaining Updated Images

<HTMLBlock>{`
<div class="callout-banner callout-banner--note">
  <span class="callout-icon"><i class="fa-duotone fa-solid fa-lightbulb"></i></span>
  <p>
    <strong>Image URL Changes</strong><br>
    With each menu published, a new version of the image URL is generated. This allows changes to the image to be updated within online menus.
  </p>
</div>
`}</HTMLBlock>

### Image URL Changes

Each menu published can generate a new version of the image URL. This helps ensure changes to the image are updated within online menus, but will apply, even if the underlying image hasn't changed. <br /><br />Integration partners can avoid re-downloading and re-processing an image on every menu publish by following one of the recommended approaches below. This will help determine when a 're-pull' of an image is actually necessary via a conditional request approach using either the Etag or the Last-Modified value;

### Option 1: ETag

1. Store the image URL alongside the `Last-Modified` header value returned when you last fetched it.
2. On each subsequent menu publish, send a conditional request with `If-Modified-Since: <Last-Modified>`.
3. Apply the same 304 / 200 handling logic as above.

### Option 2: Last-Modified

Store the image URL alongside the `Last-Modified` header value returned when you last fetched it.

| Approach          | Header sent         |
| :---------------- | :------------------ |
| **ETag**          | `If-None-Match`     |
| **Last-Modified** | `If-Modified-Since` |

### Menu Snippet

Below is a condensed menu payload showing where each image URL is located;

```json Menu Sample
[
    {
        "availabilities": [],
        "categories": [
            {
                "_id": "6579df312b1b7fb35c2cc459",
                "name": "Drinks",
                "imageUrl": "https://resizer.deliverect.com/UBcWMeTD3XSmUUH1da7NMEVi0TwWDDv9dI8unu9_xcw/rt:fill/g:ce/el:0/cb:9531913724da49749e44c1423893c002/aHR0cHM6Ly9kZWxpdmVyZWN0LWEyOGNmMmExNzc3NS5pbnRlcmNvbS1hdHRhY2htZW50cy0xLmNvbS9pL28vNzU2NTc1OTMwL2M3YTQzOTk3Y2RhMTY3ZDQxM2U2ODIwYy9tY2VjbGlwMC5wbmc=.jpg"
            }
        ],
        "channelLinkId": "66193f9dfe65ea65b85c4f93",
        "menu": "My Menu",
        "menuId": "6579df312b1b7fb35c2cc456",
        "menuImageURL": "https://resizer.deliverect.com/UBcWMeTD3XSmUUH1da7NMEVi0TwWDDv9dI8unu9_xcw/rt:fill/g:ce/el:0/cb:9531913724da49749e44c1423893c002/aHR0cHM6Ly9kZWxpdmVyZWN0LWEyOGNmMmExNzc3NS5pbnRlcmNvbS1hdHRhY2htZW50cy0xLmNvbS9pL28vNzU2NTc1OTMwL2M3YTQzOTk3Y2RhMTY3ZDQxM2U2ODIwYy9tY2VjbGlwMC5wbmc=.jpg",
        "menuType": 0,
        "modifierGroups": {
            "66193faea38a270cd82a21cd": {
                "_id": "66193faea38a270cd82a21cd",
                "name": "Choose a Sauce",
                "imageUrl": "https://resizer.deliverect.com/UBcWMeTD3XSmUUH1da7NMEVi0TwWDDv9dI8unu9_xcw/rt:fill/g:ce/el:0/cb:9531913724da49749e44c1423893c002/aHR0cHM6Ly9kZWxpdmVyZWN0LWEyOGNmMmExNzc3NS5pbnRlcmNvbS1hdHRhY2htZW50cy0xLmNvbS9pL28vNzU2NTc1OTMwL2M3YTQzOTk3Y2RhMTY3ZDQxM2U2ODIwYy9tY2VjbGlwMC5wbmc=.jpg",
                "plu": "100060",
                "productType": 3,
                "subProducts": [
                    "6618652cec388eeb3f5790b7"
                ],
                "takeawayTax": 0
            }
        },
        "modifiers": {
            "6618652cec388eeb3f5790b7": {
                "_id": "6618652cec388eeb3f5790b7",
                "name": "Truffle Cream Sauce",
                "imageUrl": "https://resizer.deliverect.com/UBcWMeTD3XSmUUH1da7NMEVi0TwWDDv9dI8unu9_xcw/rt:fill/g:ce/el:0/cb:9531913724da49749e44c1423893c002/aHR0cHM6Ly9kZWxpdmVyZWN0LWEyOGNmMmExNzc3NS5pbnRlcmNvbS1hdHRhY2htZW50cy0xLmNvbS9pL28vNzU2NTc1OTMwL2M3YTQzOTk3Y2RhMTY3ZDQxM2U2ODIwYy9tY2VjbGlwMC5wbmc=.jpg",
                "price": 800,
                "productType": 2
            }
        },
        "products": {
            "66193faea38a270cd82a21ce": {
                "_id": "66193faea38a270cd82a21ce",
                "name": "Hand Cut Fries",
                "imageUrl": "https://resizer.deliverect.com/UBcWMeTD3XSmUUH1da7NMEVi0TwWDDv9dI8unu9_xcw/rt:fill/g:ce/el:0/cb:9531913724da49749e44c1423893c002/aHR0cHM6Ly9kZWxpdmVyZWN0LWEyOGNmMmExNzc3NS5pbnRlcmNvbS1hdHRhY2htZW50cy0xLmNvbS9pL28vNzU2NTc1OTMwL2M3YTQzOTk3Y2RhMTY3ZDQxM2U2ODIwYy9tY2VjbGlwMC5wbmc=.jpg",
                "plu": "PR60",
                "posCategoryIds": [
                    "SD"
                ],
                "price": 890,
                "productType": 1,
                "subProducts": [
                    "66193faea38a270cd82a21cd"
                ]
            }
        },
        "productTags": [],
        "snoozedProducts": {}
    }
]
```

<br />

<br />
